# Work In Progress

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

## Understanding the DANDI Infrastructure

### Girder

In the [api.tf definition](https://github.com/dandi/dandi-infrastructure/blob/master/terraform/api.tf), there is reference
to a `source` keyword, where a [Terraform module called girder is defined](https://github.com/girder/terraform-heroku-girder4).

In the Girder submodule, AWS and Heroku resources are defined that facilitate base resources for compute and networking to work with DANDI Archive.

Within the DANDI Infrastructure downstream, Girder is used by declaring values that the Terraform module expects. **Resources declared by Girder cannot be overwritten**

#### Sponsored Bucket

**This is DANDI Archive specific** in which the code in `main.tf` and the presence of downstream-related files should be commented out for any clones.

A `sponsored bucket` is also declared in the `main.tf`, with downstream, related files called `sponsored_iam.tf` and `sponsored_bucket.tf`.

## Domain Management

DANDI Infrastructure manages domains for two different vendors:
- `Netlify`: Manages load balancer IPs, as well as custom domains, specifically for the UI
- `AWS Route 53`: Manages all API-based endpoints, as well as email and SSL certificate domains

### Netlify

Although Netlify prescribes mapping of Netlify-issued DNS records directly, DANDI Infrastructure relies on mapping Netlify's Load Balancer IP to the respective A Name Record in AWS Route 53, 
as prescribed in [Netlify's docs here](https://docs.netlify.com/domains-https/custom-domains/configure-external-dns/#configure-an-apex-domain)

```
resource "aws_route53_record" "gui" {
  zone_id = aws_route53_zone.dandi.zone_id
  name    = "" # apex
  type    = "A"
  ttl     = "300"
  records = ["75.2.60.5"] # Netlify's load balancer, which will proxy to our app
}
```

Note the code blob above, as referenced from [DANDI Infrastructure domain.tf Terraform template](https://github.com/dandi/dandi-infrastructure/blob/master/terraform/domain.tf#L13).

### AWS Route 53

## AWS Buckets

While [Girder](https://github.com/girder/terraform-heroku-girder4) does declare S3-based resources, configuration is still needed within DANDI Infrastructure.

Find your AWS Account ID. This value will be referenced in the `main.tf` Terraform template

<br/><br/>
<img
src="../img/aws_account.png"
alt="aws_account"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Populate the value in the [appropriate account ID reference](https://github.com/dandi/dandi-infrastructure/blob/master/terraform/main.tf#L14) in the `main.tf` template.

### Staging vs. Production

### Email Setup

TBD

## Manual Steps in the AWS Console and Netlify
