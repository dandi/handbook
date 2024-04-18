# Work In Progress

## Setting up your GitHub OAuth Account

Please follow the steps in [Initialize Vendors - GitHub](../60_initialize_vendors/#github) to get started.

For the next steps in setting up authentication, you'll want to record the values
created during [Obtaining your Oauth App creds](..60_initialize_vendors/#obtaining-your-oauth-app-credentials).

## Creating "Sites" and "Social App" in DANDI Archive Admin Panel

*In order to complete this step, you will need to have deployed an initial DANDI Archive API -- see here for more details [Creating the DANDI Archive API](../64_dandi_archive)

First, sign in via the Django admin panel with your credentials created via the [Creating an admin user account for the DANDI Archive API step](../64_dandi_archive/#creating-a-django-superuser-admin-account)

The Django Admin panel should be located at: `<your_full_api_url/admin`

<br/><br/>
<img
src="../img/admin_panel.png"
alt="admin_panel"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Next, you'll want to proceed to the `Sites' tab -- create 2 sites, one for your UI, and another for your API domain

<br/><br/>
<img
src="../img/site_admin.png"
alt="site_admin"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Next, you'll want to proceed to the `Social applications` tab, located on the left side panel. Once in this panel, you'll need to click
`Add Social Application` in the top right corner

<br/><br/>
<img
src="../img/social_app_panel.png"
alt="social_app_panel"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Once in this panel, you'll want to create a `Social Application` object with:

• The Provider as `GitHub`
• The client ID as your GitHub OAuth client ID
• The client secret as your GitHub OAuth client secret
• Two `Sites` objects -- these objects you should have created a few steps prior

After creating this object, you are all set in the Django Admin panel for now.

## Populating appropriate values for the frontend to handle authentication



## Configuring Migrations for Initial Auth Setup



