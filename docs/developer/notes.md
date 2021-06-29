# Developer Notes

This page contains crucial information for anyone starting work on the DANDI
project.

# Overview

The DANDI archive dev environment comprises three major pieces of software:
`dandi-api`, `dandiarchive`, and `dandi-cli`.

[`dandi-api`](https://github.com/dandi/dandi-api) is a Django application that
serves the DANDI REST API. The Django application makes use of several services
to provide essential function for the API, including Postgres (to hold
administrative data about the web application itself), Celery (to run
asynchronous compute tasks as needed to implement API semantics), and RabbitMQ
(to act as a message broker between Celery and the rest of the application).

The easiest way to run the API along with its services is through a Docker
Compose setup, as detailed in the [`dandi-api` README](https://github.com/dandi/dandi-api#readme).

[`dandiarchive`](https://github.com/dandi/dandiarchive) is the web frontend
application; it connects to `dandi-api` and provides a user interface to all of
the DANDI functionality. `dandiarchive` is a standard web application built with
`yarn`. See the [`dandiarchive` README](https://github.com/dandi/dandiarchive#readme)
for instructions on how to build it locally.

[`dandi-cli`](https://github.com/dandi/dandi-cli) is a Python command line tool
used to manage downloading and uploading of data with the archive. You may need
to make use of this tool in developing new features for the frontend and
backend, but there are other methods of faking data in the system to work with
as well. You can install `dandi-cli` with a command like `pip install dandi`
(then invoke `dandi` on the command line to run the tool), or build it locally
following the instructions in the [`dandi-cli` README](https://github.com/dandi/dandi-cli#readme).

# Important Things to Know

This section gathers some important yet small bullet points of knowledge, useful
to dive into development on the DANDI project.

## Technologies Used

This section details some of the foundational technologies used in the DANDI
codebases. Some basic understanding of these technologies is the bare minimum
requirement for contributing meaningfully, but keep in mind that the DANDI team
can help you get spun up as well.

### `dandiarchive`

**JavaScript/TypeScript.** The DANDI archive code is a standard JavaScript web
application, but we try to implement new functionality using TypeScript.

**Vue/VueX.** The application's components are written in Vue, and global
application state is managed through VueX.

**Vuetify.** The components make heavy use of the Vuetify component library.

For general help with `dandiarchive`, contact @waxlamp.

### `dandi-api`

**Python3.** The backend code is written in Python 3.

**Django/drf/drf-yasg.** The API infrastructure is implemented through a Django application.
This means that application resources must be mapped to Django models, while
Django views mediate API responses. The REST endpoints are implemented via
Django Rest Framework (DRF), while DRF-YASG is used to generate Swagger
documentation.

For general help with `dandi-api`, contact @waxlamp.

## Deployment

The DANDI project uses automated services to continuously deploy both the
`dandi-api` backend and the `dandiarchive` frontend.

Heroku manages backend deployment automatically from the `master` branch of the
`dandi-api` repository. For this reason it is important that pull requests pass
all CI tests before they are merged. Heroku configuration is in turn managed by
Terraform code stored in the `dandi-infrastructure` repository. If you need
access to the Heroku DANDI organization, talk to @satra.

Netlify manages the frontend deployment process. Similarly to `dandi-api`, these
deployments are based on the `master` branch of `dandiarchive`. The
[`netlify.toml` file](https://github.com/dandi/dandiarchive/blob/master/netlify.toml)
controls Netlify settings. The @dandibot GitHub account is the "owner" of the
Netlify account used for this purpose; in order to get access to that account,
speak to @satra.

## Code Hosting

All code repositories are hosted on GitHub. The easiest way to contribute is to
gain push access to the repositories by talking to @waxlamp; this way, you can
create pull requests based on branches within the origin repositories, which in
turn allows for Netlify deploy previews and Heroku staging previews to be built.

However, this is not strictly required. You can contribute using the standard
fork-and-pull-request model, but under this workflow we will lose the benefit of
those previews.

## Email Lists

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

If you need the credentials for logging into ImprovMX, speak to [Roni
Choudhury](roni.choudhury@kitware.com).

## Miscellaneous Tips and Information

### Use email address to log into dev Django admin panel

Once `dandi-api` is up and running, you can access the Django admin panel at
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
mit.edu processes emails, and does not occur in general for, e.g., messages sent
from the API server to users.
