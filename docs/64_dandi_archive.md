# Work In Progress

This step assumes that you have completed all steps in: [Initialize Vendors](../60_initialize_vendors) & [DANDI Infrastructure](../63_dandi_infrastructure)

## Initial Steps

### Running terraform apply upon dandi-infrastructure for the first time

Resources (e.g. the servers and environment ) for DANDI Archive are provisioned upon applying the Terraform definitions in
`dandi-infrastructure`, specifically in the [api.tf definition](https://github.com/dandi/dandi-infrastructure/blob/master/terraform/api.tf)
The resources won't be running anything until your first Heroku `release` upon the Heroku app

To see how your code would translate into a new `Heroku` release, [see the GitHub actions workflow used by DANDI Archive here](https://github.com/dandi/dandi-archive/blob/master/.github/workflows/backend-production-deploy.yml)

## Understanding the concept of the Procfile for Heroku

Heroku initializes compute on servers (known as `dynos` in Heroku land). Each `dyno` that you have runs a process.
Which process, the resources allocated to that process, and how that process is run, is defined in a `Procfile`

DANDI Archive defines a [Procfile](https://github.com/dandi/dandi-archive/blob/master/Procfile). In this `Procfile`,
you'll see several entries:

- `release`: a command that is run each time a new version of DANDI API is pushed to Heroku.
- `web`: runs `gunicorn`, a persistent server that handles HTTP requests for the DANDI API.
- `worker`: a worker process that runs `celery` behind-the-scenes. `celery` handles tasks that would otherwise cause the API to timeout.
- `checksum-worker`: another worker, also using `celery`, that specifically calculates if a new file pushed to DANDI Archive is new/updated, and determines what exactly has been changed.
- `analytics-worker`: another `celery` worker that handles all tasks related to processing of S3-related logs.

This `Procfile` shouldn't need to be changed or reconfigured much for a DANDI-clone; however, it is important to note so that one may understand how DANDI Archive is working.

## Understanding metrics and logging via Heroku

Heroku provides observability in a very convenient manner. If you'd like to see what is happening with your app in real-time, simply access the options shown in the image below

<br/><br/>
<img
src="../img/metrics_heroku.png"
alt="metrics_heroku"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

### Configuring email alerts via Heroku

Heroku will send relevant updates for any concerning behavior/downtime/etc. to your email. Be sure to configure this, as it is a manual step.

You'll find options in the `Access` tab

<br/><br/>
<img
src="../img/members_heroku.png"
alt="members_heroku"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

## Creating a Django "superuser" (Admin) Account

Django has the concept of a `superuser` -- essentially an `administrator` user type. For steps such as [setting up authentication for DANDI Archive](../61_dandi_authentication/#creating-sites-and-social-app-in-dandi-archive-admin-panel) 
you'll need to set up a `superuser` account.

Go into your Heroku app, and identify the `Run Console` option:

<br/><br/>
<img
src="../img/heroku_console.png"
alt="heroku_console"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Initialize a `bash` session

<br/><br/>
<img
src="../img/heroku_bash.png"
alt="heroku_bash"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

Once in the console, run a quick `ls` to ensure that you can see the `manage.py` file. The `manage.py` file is Django's entrypoint to a handful of management commands.

You'll now want to create a `superuser`

<br/><br/>
<img
src="../img/heroku_user.png"
alt="heroku_user"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
<br/><br/>

You'll be prompted to create a user -- **Note: use an email that is not associated with your GitHub account, as GitHub is the default authentication provider for DANDI Archive**.

To do one final test, try using your credentials to log into the Django Admin panel -- it should be located at `/admin` for your API, such as `your-apps-domain.com/admin`

You are all set here!

## Frontend Deployment

A majority of the necessary setup steps here are defined already [during the vendor account setup for Netlify](../60_initialize_vendors/#netlify).

The only other major initial setup step for the DANDI Archive frontend is regarding authentication -- [see here for more details](../61_dandi_authentication/#populating-appropriate-values-for-the-frontend-to-handle-authentication)

## Updating Allowed Hosts

## Approval of Users

## Setting up Staging Environments