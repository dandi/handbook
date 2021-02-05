# Project structure

The DANDI project is organized around several Github repositories. The
main ones are the following.

1. **The DANDI archive.** This [repository](https://github.com/dandi/dandiarchive)
contains the code for deploying the archive. It includes the client-side Web
application frontend based on the [Vuejs](https://vuejs.org/) framework, the
server backend extensions to [the Girder platform](https://girder.readthedocs.io/en/latest/),
and the deployment code for pushing changes to the archive as they are merged in.

1. **The DANDI Python client.** This [repository](https://github.com/dandi/dandi-cli)
contains the code for the command line tool used to interact with the archive.
It allows you to download data from the archive. It also allows you to locally
organize and validate your data before uploading to the archive.

1. **The DANDI Jupyterhub.** This [repository](https://github.com/dandi/dandihub)
contains the code for deploying a Jupyterhub instance to support interaction
with the DANDI archive.

1. **The DANDI API.** This [repository](https://github.com/dandi/dandi-publish)
provides the code for the DANDI API.

1. **The DANDI schema.** This [repostiory](https://github.com/dandi/schema)
provides the details and some supporting code for the DANDI metadata schema.

1. **The DANDI handbook.** This [repository](https://github.com/dandi/handbook)
provides the contents of this website.

1. **The DANDI Website.** This [repository](https://github.com/dandi/dandi.github.io)
provides an overview of the DANDI project and the team members and collaborators.
