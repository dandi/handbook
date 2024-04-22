# Work In Progress

## Understanding the DANDI Infrastructure

### Girder

### AWS Buckets

### Domain Management

### Staging vs. Production

## Configuring Terraform

[First, make sure you have properly set up your Terraform Cloud account and linked the account to the proper GitHub repository](../60_initialize_vendors/#terraform-cloud)

To double-check whether your GitHub repository is properly linked, proceed to the `Version Control` tab.

The `Version Control` Repository value should point to the repository, and the `Terraform Working Directory` should point to `terraform` 

<br/><br/>
<img
src="../img/terraform_config.png"
alt="terraform_config"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

## Applying Terraform

There are two ways in which you can invoke `terraform plan` and `terraform apply` upon your infrastructure.

### Automatic Run Triggering

This is set to occur by default when you connect a GitHub repository to Terraform Cloud. After pushing code to your repository,
Terraform will run `terraform plan`, generating a summary of what will happen if you were to run `terraform apply`. 

**Note: `terraform apply` will not be run automatically (this is good!), so be sure to review and check prior to applying.

To view, go to the `Runs` tab -- you will see that the Terraform run populates the GitHub code action above

<br/><br/>
<img
src="../img/terraform_auto.png"
alt="terraform_auto"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

### Trigger Run from UI manually

If you'd like more control over Terraform, you can also default to run manually.

<br/><br/>
<img
src="../img/terraform_manual.png"
alt="terraform_manual"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

## Manual Steps in the AWS Console and Netlify



## Setting up Email

TBD