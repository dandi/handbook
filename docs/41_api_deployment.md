## Initial Steps

This section assumes that you have completed all steps in [Linc Development > Initialization](./40_initialization.md)

For the purpose of LINC coupling to DANDI Archive, you'll first want to fork the [dandi-infrastructure](https://github.com/dandi/dandi-infrastructure) repository.

## Understanding "dandi-infrastructure"

`dandi-infrastructure` is a repository containing a handful of Terraform configuration files. The baseline for all these files; however, is an external library, known as `girder`.
`girder` is a series of Terraform modules maintained by [Kitware](https://kitware.com/)

`girder` is sub-divided further into specific Terraform providers that interact with the module. In the case of LINC Brain, 

First Steps for Deployment of Staging API
============================================
• In your relevant Terraform GitHub repository, enter a new `project_slug` within `api.tf` in the `api` section -- this will be the name of the application that will be initialized in Heroku

• (For staging), go into your Dandi Archive-related, and alter the application name in the "Create Heroku Build" step `backend-staging-deploy.yml` GitHub Action Workflow

• Next, run your Terraform Plan via Terraform Cloud -- a shortcoming of the current setup is that the Deployment will initially fail
- You'll next need to "Deploy" the Dandi-related Archive app via the `backend-staging-deploy.yml` workflow

• Next, run your Terraform Plan one more time
- This will notice the `Procfile` in your Dandi-related Archive, in which the appropriate Heroku Dyno workers will then be properly provisioned

• The API working correctly relies on a handful of infrastructure being set up, as well as specific authentication variables being set....
