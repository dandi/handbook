# Initialize Vendor Accounts

This series of documents explains how to create a new instance of the DANDI project (i.e. a clone of the DANDI Archive). It is suggested that you briefly read through each of the
documents in this guide before starting.

The DANDI ecosystem relies on vendor services to operate.  So first you will need to set up accounts with the following vendors:

• **Heroku**

• **AWS**

• **GitHub**

• **Terraform Cloud**

• **Netlify**

• **Sentry**

• **PyPI**

• **Datalad (TBD)**

• **git-annex (TBD)**

## Heroku

##### Create your own Heroku account

No special steps here, just create!

##### Create a "Team" 

Send invites to the appropriate e-mail addresses to onboard your team

##### Create an "App"

<br/><br/>
<img
src="../img/heroku_create_app.png"
alt="heroku_create_app"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You can name whatever you wish -- no need to add a pipeline, etc. **Be sure to note the app name**

<br/><br/>
<img
src="../img/heroku_app_name.png"
alt="heroku_app_name"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Your app will be an empty template, but that is OK -- more to come here!

##### Obtain Heroku API Key

You'll need to provide access to Heroku for GitHub, Terraform, etc. -- thus, you'll need to generate an API Key

First go to your `Account Settings`:

<br/><br/>
<img
src="../img/heroku_settings.png"
alt="heroku_app_name"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Next, find the `API Key` section and generate a new key.

<br/><br/>
<img
src="../img/heroku_key.png"
alt="heroku_app_name"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Keep this value for further steps.

## AWS

##### Create your organization's AWS account

No special steps here, just create!


##### Create an IAM User Group with `AdministratorAccess`

<br/><br/>
<img
src="../img/user_group.png"
alt="user_group"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Ensure that you click the right policy in the `Attach permissions policies` section.

<br/><br/>
<img
src="../img/permissions.png"
alt="permissions"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

**Note: If you know more refined permissions to give the IAM Group, that is preferred, as those with access
to the credentials of `AdministratorAccess` in AWS can be an extreme security hazard if not managed appropriately**

<br/><br/>
<img
src="../img/create_group.png"
alt="create_group"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>


##### Create an IAM user that lives in the User Group you made

<br/><br/>
<img
src="../img/create_user.png"
alt="create_user"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Next, give a unique name -- no need to enable Console Access

<br/><br/>
<img
src="../img/specify_user.png"
alt="specify_user"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Lastly, add them to the Group you made in the step above:

<br/><br/>
<img
src="../img/add_perms.png"
alt="add_perms"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Create security credentials

You'll need to create `Security Credentials` for your User -- these credentials will be specifically used
in your `Terraform Cloud` setup

Firstly, go to your User and click the `Security Credentials` tab:

<br/><br/>
<img
src="../img/creds.png"
alt="creds"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>

Navigate to `Create access key`

<br/><br/>
<img
src="../img/access_key.png"
alt="access_key"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You'll be prompted to provide a reason for the access key creation. It doesn't matter much, so `Other` is a completely acceptable choice

<br/><br/>
<img
src="../img/creds_purpose.png"
alt="creds_purpose"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Time to create the key!

<br/><br/>
<img
src="../img/create_tag.png"
alt="create_tag"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You'll be provided with the values of your `Access key` and `Secret access key` -- store these values somewhere secure and accessible

<br/><br/>
<img
src="../img/retrieve.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

## GitHub

You'll need to create a GitHub Organization with your DANDI fork. [See here for documentation to create a GitHub organization](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch)

##### Initialize your OAuth App

Once you create the Organization, navigate to the `Settings` tab:

<br/><br/>
<img
src="../img/github_home.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Under `Settings`, you'll want to initialize an `OAuth App` -- navigate to `Developer settings > OAuth Apps`

<br/><br/>
<img
src="../img/oauth_app.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Click on `New Org OAuth App` next

<br/><br/>
<img
src="../img/new_app.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You'll be prompted with the following form -- see the example values populated in this screenshot -- more to come in other sections for where these values might be populated:

<br/><br/>
<img
src="../img/register_new.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Obtaining your OAuth App Credentials

After creating your OAuth App, you'll lastly want to obtain a client secret key and your client ID -- make sure to note these values for further steps when creating our API

<br/><br/>
<img
src="../img/client_values.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Connecting GitHub with Heroku

**This step is contingent that you have forked [dandi-archive](https://github.com/dandi/dandi-archive)**

Once you have the repository forked, you'll want to navigate to `Settings` in the repository page:

<br/><br/>
<img
src="../img/linc_settings.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Next, navigate to `Security > Secrets and variables > Actions`

<br/><br/>
<img
src="../img/secrets_actions.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

And then lastly create two new secrets, `HEROKU_EMAIL` should be the email address/account you used to generate your `HEROKU_API_KEY`

<br/><br/>
<img
src="../img/heroku_secrets.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

## Terraform Cloud

Terraform is configuration tool for managing "infrastructure-as-code" -- meaning that we can programatically manage infrastructure in
a traceable, version-controlled form.

The Terraform ecosystem provides a UI tool called **Terraform Cloud**

Start by visiting `https://app.terraform.io/` and making an account.

##### Creating a Terraform Project and Workspace

Once you have successfully made an account, you'll want to create a `Workspace` and a `Project` in that `Workspace`

<br/><br/>
<img
src="../img/terraform_init.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Populate Environment Variables

After successful creation, you'll want to populate the following variables in the `Variables` section of the `Workspace`:

You'll need to populate `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `HEROKU_API_KEY` and `HEROKU_EMAIL`

<br/><br/>
<img
src="../img/terraform_vars.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Link GitHub Repository

Next, link your appropriate GitHub repository, in this case, most likely your fork of [dandi-infrastructure](https://github.com/dandi/dandi-infrastructure).

<br/><br/>
<img
src="../img/tf_vcs.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Link your repository -- you may need to declare the appropriate subdirectory 

<br/><br/>
<img
src="../img/tf_repo.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You can now invoke Terraform `plan` and `apply` from the Terraform Cloud UI or via your GitHub repository Actions.

## Netlify

The frontend for `dandi-archive` is served via [Netlify](https://www.netlify.com/)

##### Create Account and Initialize Project

First, create an account. After creating an account, you'll want to navigate to `Sites`, where you can `Add a new site`, and then `Import an existing project`

<br/><br/>
<img
src="../img/start_netlify.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You'll want to next connect `dandi-archive` via `Deploy with GitHub`. Enable Netlify to be authorized as a GitHub app. Once you have
enabled authorization, you'll need to specifically link your appropriate repositories:

<br/><br/>
<img
src="../img/netlify_auth.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Now once you see the appropriate repository, you'll want to navigate to configure where Netlify can find and build your site

<br/><br/>
<img
src="../img/netlify_repo_search.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

For usage of Netlify, one could refer to declaring a `netlify.toml` configuration file [like the one referenced in DANDI Archive](https://github.com/dandi/dandi-archive/blob/master/web/netlify.toml)

These values can also be replicated in the settings. 

<br/><br/>
<img
src="../img/netlify_config.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Your frontend should be able to deploy to a auto-generated URL via Netlify now! Steps for domain management and configuration are described further in the [Frontend Deployment](.
./42_frontend_deployment) section of these docs.

## Sentry

[Sentry](https://sentry.io/) is a monitoring tool used for the DANDI Archive API. It is integral in order to notify engineers if a system is down, experiencing poor performance, or may have unwanted users

Begin by creating a Sentry account -- once successful, you'll start by creating a new Project:

<br/><br/>
<img
src="../img/sentry_init.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Select Django as an App Type

DANDI Archive API is built as a Django app -- so proceed to select `Django` on the following screen:

<br/><br/>
<img
src="../img/sentry_django.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

##### Capture Sentry DSN value

You'll be provided with a screen displaying how to initialize and install Sentry into your Django app. For now, just capture the DSN value.
This value will be used later as an environment variables while deploying your API via Terraform

<br/><br/>
<img
src="../img/sentry_sdk_dsn.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

## PyPI

A common way that users interact with the DANDI ecosystem is via its CLI and Python client tool: [dandi-cli](https://pypi.org/project/dandi/)

##### Create a PyPI Account

Versions of this tool are hosted, versioned and managed by PyPI -- therefore, you will need to create an account.

##### Retrieve an API Token

After creating an account, you'll want to create your own API key -- first go to `Account settings`

<br/><br/>
<img
src="../img/pypi_account.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Scroll down to `API tokens` and create a value -- keep track of this value for now. We will use it later

<br/><br/>
<img
src="../img/pypi_api_token.png"
alt="retrieve"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

In terms of creating and publishing your first project, go to the [documentation for setting up a CLI and Python Client](.
./47_cli_python)


## datalad (TBD)

## git-annex (TBD)