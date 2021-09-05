# Terraform
terraform allows to have all the cloud infrastructure setup in one config file

### Terraform best practices

* do not edit json config file manually, use  terraform commands
* share the terraform.tstate file in a shared place so every team member can update
* lock the file to avoid two people writing at the same time (set up on s3 storage)
* backup the file (with version control on s3)
* use one .tstate file for each env like dev test prod.. etc

* for terraform code   use    GitOps: infrastructure as Code  IaC
    * save .tstate file on a dedicated git repository
    * using Continuous Integration review and test practices
    * update changes on Continuous Deploy only (after test are passed)
