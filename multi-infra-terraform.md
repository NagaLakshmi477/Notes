multiple-infra-using-terraform:
===========================
dev,prod,qa,sit,uat,pre-prod

lakshmireddy.site

roboshop-dev-mongodb
roboshop-dev-redis
roboshop-dev-mysql


roboshop-UAT-mongodb
roboshop-UAT-redis
roboshop-UAT-mysql

roboshop-PROD-mongodb
roboshop-PROD-redis
roboshop-PROD-mysql
sites:
mongodb-dev.lakshmireddy.site

tfvars: we can override the value throught tfvars 

How to run provisioners:
-----------------------

terraform init -backend-config=dev/backend.tf
terraform plan -var-file=dev/dev.tfvars
terraform apply -var-file=dev/dev.tfvars

if you want to change to prod
----------------------
terraform init -reconfigure -backend-config=prod/backend.tf
terraform plan -var-file=prod/prod.tfvars
terraform apply -var-file=prod/prod.tfvars


pros:
====
no need to duplicate the code
consitency

cons:
====
should be very cautious change done in DEV may go to prod alos by mistake



workspace:
========
workspace means multiple environements
creating workspace 
terraform workspace --> it will give all options

Usage: terraform [global options] workspace

  new, list, show, select and delete Terraform workspaces.

Subcommands:
    delete    Delete a workspace
    list      List Workspaces
    new       Create a new workspace
    select    Select a workspace
    show      Show the name of the current workspace


terraform workspace new dev  ----> to create 
select workspace:
terraform workspace select dev
terraform.workspace=dev/prod
lookup(map,key) ---> dev
lookup(map,qa,"t3.micro") 

terraform workspace select prod
