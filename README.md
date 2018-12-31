cloud composer Terraform
========================

Terraform module for provisioning and configuring google cloud composer instance and configure environment variables and install python packages.


Pre-requiestes
==============

1. Install and configure Terraform. You can follow the steps in following [URL](https://learn.hashicorp.com/terraform/getting-started/install) to install Terraform 

2. Create a service account for creating cloud composer instance with cloud composer worker IAM role.

3. Update the path to service account in terraform main file.


Variables
=========

| Variable                  | Type   | Comment                      |
|---------------------------|--------|------------------------------|
| google_project_id         | string | GCP project name             |
| name                      | string | Cloud composer instance name |
| region                    | string | GCP compute node region      |
| zone                      | string | GCP compute zone             |
| machine_type              | string | GCP node machine type        |
| email                     | string | Airflow alert mail address   |
| sendgrid_api_key          | string | API key for sendgrid         |
| oauth_scopes              | list   | oauth_scopes                 |
| airflow_config_overrides  | map    | airflow_config_overrides     |
| pypi_packages             | map    | pypi_packages                |
 

How to create an enviornment
============================

1. You can a use the following snippet to create the cloud composer environment.

```
provider "google" {
    credentials = "${file("account.json")}"
    project = "dl-redash"
    zone = "us-central1-c"
}

module "composer" {
 source = "github.com/bmv3cg/cloud-composer"
  google_project_id = "replace with your GCP project name" 
  name = "cloud-composer-tf"  
  zone= "us-central1-c"
  region = "us-central1"
  machine_type = "n1-standard-1"
  sendgrid_api_key = "api key"
}
```

2. You can intiate a Terrafrom module and provider using the command. This will download and configure all the dependencies for installation.

```
terraform init
```

3. Customize the template as per your requirements. After confirming the plan you can run the apply the plan using the following  execute the deployment.

```
terrafrom apply 
```

Misc
===

Cloud composer provisioning takes around 10 to 15 minutes to complete, but if you are using custom environment changes and python modules it will nearly take 45 minutes to complete the deployment.
