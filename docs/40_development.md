This page contains crucial information for anyone starting work on the DANDI
project.

## Project Structure

The DANDI project is organized around several GitHub repositories. The
main ones are the following.

### Helpdesk (/helpdesk)

The [dandi/helpdesk repository](https://github.com/dandi/helpdesk)
contains our community help platform. You can submit [issues](https://github.com/dandi/helpdesk/issues/new/choose)
or [questions for discussion](https://github.com/dandi/helpdesk/discussions).

### Archive (/dandi-archive)

The [dandi/dandi-archive repository](https://github.com/dandi/dandi-archive)
is the code of the client-side Web application which is deployed at 
[dandiarchive.org](https://dandiarchive.org) **and** DANDI REST API deployed at 
[api.dandiarchive.org](https://api.dandiarchive.org). 
It is based on the [Vuejs](https://vuejs.org/) framework for Web UI frontend and Django
to run the DANDI REST API. See the [`dandi-archive` README](https://github.com/dandi/dandi-archive#readme)
for instructions on how to build it locally.

The Django application makes use of several services
to provide essential function for the DANDI REST API, including Postgres (to hold
administrative data about the web application itself), Celery (to run
asynchronous compute tasks as needed to implement API semantics), and RabbitMQ
(to act as a message broker between Celery and the rest of the application).

The easiest way to run the API along with its services is through a Docker
Compose setup, as detailed in the [Develop with Docker quickstart](https://github.com/dandi/dandi-archive/blob/master/DEVELOPMENT.md).

#### More on technologies used

**JavaScript/TypeScript.** The DANDI archive code is a standard JavaScript web
application, but we try to implement new functionality using TypeScript.

**Vue/VueX.** The application's components are written in Vue, and global
application state is managed through VueX.

**Vuetify.** The components make heavy use of the Vuetify component library.

**Python3.** The backend code is written in Python 3.

**Django/drf/drf-yasg.** The API infrastructure is implemented through a Django application.
This means that application resources must be mapped to Django models, while
Django views mediate API responses. The REST endpoints are implemented via
Django Rest Framework (DRF), while DRF-YASG is used to generate Swagger
documentation.

**S3.** Data is hosted on AWS S3 buckets in main deployments, and on [Minio](https://min.io/) for local testing etc.

For general help with `dandi-archive`, contact @waxlamp.

#### Deployment

The DANDI project uses automated services to continuously deploy both the
frontend and API backend from the `dandi-archive` repository.

Heroku manages backend deployment automatically from the `master` branch of the
`dandi-api` repository. For this reason it is important that pull requests pass
all CI tests before they are merged. Heroku configuration is in turn managed by
Terraform code stored in the `dandi-infrastructure` repository. If you need
access to the Heroku DANDI organization, talk to @satra.

Netlify manages the frontend deployment process. These
deployments are based on the `master` branch of `dandi-archive`. The
[`netlify.toml` file](https://github.com/dandi/dandi-archive/blob/master/web/netlify.toml)
controls Netlify settings. The @dandibot GitHub account is the "owner" of the
Netlify account used for this purpose; in order to get access to that account,
speak to @satra.

### Python client (/dandi-cli)

The [dandi/dandi-cli repository](https://github.com/dandi/dandi-cli)
contains the code for the command line tool used to interact with the archive.
It allows you to download data from the archive. It also allows you to locally
organize and validate your data before uploading to the archive.

You may need to use this tool when developing new features for the frontend and
backend, but there are other methods of faking data in the system to work with
as well. You can install `dandi-cli` with a command like `pip install dandi`
(then invoke `dandi` on the command line to run the tool), in conda using
`conda install -c conda-forge dandi`, or build it locally following the
instructions in the [`dandi-cli` README](https://github.com/dandi/dandi-cli#readme).

### Metadata schema Python library (/dandi-schema)

The [dandi/dandi-schema repository](https://github.com/dandi/dandi-schema)
establishes the metadata schema and the Python library (`dandischema`, available from PyPI and conda-forge) which are
used by other components of DANDI: DANDI archive and DANDI Python client to update and validate metadata records. 

[`dandi-schema`](https://github.com/dandi/dandi-schema) is a Python library for 
creating, maintaining, and validating the DANDI metadata models for dandisets 
and assets. You may need to make use of this tool when improving models, or 
migrating metadata. You can install `dandischema` with a command like 
`pip install dandischema`.

### Metadata schema release exports (/schema)

Releases of the metadata schema in aforementioned `dandi-schema` are also automatically serialized as JSON schema for each release and stored in the [dandi/schema repository](https://github.com/dandi/schema/).
Those serializations could be used to build Web UIs based on JSON schema descriptions and validation of metadata using JSON schema validator.

### Computing Hub (/dandi-hub)

The [dandi/dandi-hub repository](https://github.com/dandi/dandi-hub)
contains the code for deploying a JupyterHub instance to support interaction
with the DANDI archive.

### Handbook (/handbook)

The [dandi/handbook repository](https://github.com/dandi/handbook)
provides the contents of this website.
It aims to provide documentation for users and developers of DANDI.

### "About" website (/dandi.github.io)

The [dandi/dandi.github.io repository](https://github.com/dandi/dandi.github.io)
provides an overview of the DANDI project and the team members and collaborators.

### DataLad Dandisets (/dandisets)

The [dandi/dandisets repository](https://github.com/dandi/dandi.github.io) is a [DataLad](https://datalad.org)
super-dataset which provides DataLad sub-datasets (via git submodules) for each Dandiset in the DANDI archive.
Individual DataLad dandisets are all contained within [github.com/dandisets organization](https://github.com/dandisets)
and could also be installed/cloned independently using DataLad or directly using git and git-annex.
DataLad datasets provide an alternative access mechanism to data in DANDI archive via version control systems
to facilitate efficient access, discovery of dandisets and assets changes history, etc.
[datalad-fuse](https://github.com/datalad/datalad-fuse) extension could also be used
on those DataLad datasets to provide efficient sparse access via Python API or FUSE filesystem on GNU Linux systems.

## Code Hosting

All code repositories are hosted on GitHub. The easiest way to contribute is to
gain push access to the repositories by talking to @waxlamp; this way, you can
create pull requests based on branches within the origin repositories, which in
turn allows for Netlify deploy previews and Heroku staging previews to be built.

However, this is not strictly required. You can contribute using the standard
fork-and-pull-request model, but under this workflow we will lose the benefit of
those previews.

## Mailing Lists

The project's email domain name services are managed via Terraform as AWS Route
53 entries. This allows the API server to send emails to users, etc. It also
means we need a way to forward incoming emails to the proper mailing list--this
is accomplished with a service called [ImprovMX](https://improvmx.com/).

The email addresses info@dandiarchive.org and help@dandiarchive.org are
advertised to users as general email addresses to use to ask for information or
help; both of them are forwarded to dandi@mit.edu, a mailing list containing the
leaders and developers of the project. The forwarding is done by the ImprovMX
service, and more such email addresses can be created as needed within that
service.

If you need the credentials for logging into ImprovMX, speak to Roni
Choudhury (<roni.choudhury@kitware.com>).

## Miscellaneous Tips and Information

### Use email address to log into dev Django admin panel

Once `dandi-archive` is up and running, you can access the Django admin panel at
http://localhost:8000/admin. The login page asks for a "username" but really it
is expecting the email address associated with the username.

One easy trick here is to supply the username again as the email address when
you are setting up the superuser during initial setup.

### Refresh GitHub login to log into prod Django admin panel

To log into the production Django admin panel, you must simply be logged into
the DANDI Archive production instance using an admin account.

However, at times the Django admin panel login seems to expire while the login
to DANDI Archive proper is still live. In this case, simply log out of DANDI,
log back in, and then go to the Django admin panel URL
(e.g., https://api.dandiarchive.org/admin) and you should be logged back in
there.

### Why do incoming emails to dandiarchive.org look crazy?

When a user emails help@dandiarchive.org or info@dandiarchive.org, those
messages are forwarded to dandi@mit.edu (see [above](#email-lists)) so that the
dev team sees them. However, these emails arrive with a long, spammy-looking
From address with a Heroku DNS domain; this seems to be an artifact of how
mit.edu processes emails, and does not occur in general (e.g. messages sent
from the API server to users).
