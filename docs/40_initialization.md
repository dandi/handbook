LINC Brain relies on a handful of vendor services to operate:

The following accounts must be made to create LINC Brain in a production setting:

• **Heroku**

• **AWS**

• **GitHub**

• **Terraform Cloud**

• **Netlify**

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

AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY

## GitHub

You'll need to create a GitHub Organization with your DANDI fork. [See here for documentation to create a GitHub organization](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch)

## Terraform Cloud

Terraform is configuration tool for managing "Infrastructe-as-code" -- meaning that we can programatically manage infrastructure in
a traceable, version-controlled form.

The Terraform ecosystem provides a UI tool called **Terraform Cloud**

##### Create an Account

- Create a new Project and a Workspace within that Project
- Populate the 'Variables' in the Workspace with the following
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- HEROKU_API_KEY
- HEROKU_EMAIL
- Link your GitHub repository -- ensure that Terraform Cloud can find your .tf templates (you may need to alter the subdirectory it looks for)
- In your GitHub repository also populate GitHub Actions Secrets with the HEROKU_API_KEY, HEROKU_EMAIL

## Netlify