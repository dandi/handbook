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

<br/><br/>
<br/><br/>
##### Create a "Team" 

Send invites to the appropriate e-mail addresses to onboard your team

<br/><br/>
<br/><br/>
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

<br/><br/>
<br/><br/>
## AWS

##### Create your organization's AWS account

No special steps here, just create!

<br/><br/>
<br/><br/>

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

<br/><br/>
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

<br/><br/>
<br/><br/>

4. **Create security credentials, note the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY**


3. Create Terraform Cloud account
    - Create a new Project and a Workspace within that Project
    - Populate the 'Variables' in the Workspace with the following
        - AWS_ACCESS_KEY_ID
        - AWS_SECRET_ACCESS_KEY
        - HEROKU_API_KEY
        - HEROKU_EMAIL
    - Link your GitHub repository -- ensure that Terraform Cloud can find your .tf templates (you may need to alter the subdirectory it looks for)
        - In your GitHub repository also populate GitHub Actions Secrets with the HEROKU_API_KEY, HEROKU_EMAIL

4. Create a Netlify account