# Developers information

## Current deployed instance

Uses Girder as a backend for storing dandisets on S3 in `s3://dandiarchive` with Girder keystore under `girder-assetstore/`

### https://github.com/dandi/dandiarchive - Web UI

- https://gui.dandiarchive.org/ is the deployed web UI instance 

### https://github.com/dandi/dandi-cli/ - CLI/Python client

To be installed via `pip` or `conda` to interact with the archive.

### https://github.com/dandi/redirector - redirector

which provides redirects from https://dandiarchive.org/


## In development

It will use dandi-api service/backend which would provide specialized to dandiarchive functionality to 
upload/download dandisets and public releases.  All data ATM goes into a private bucket but later will migrate to 
use `s3://dandiarchive`

### https://github.com/dandi/dandiarchive - Web UI

The same repository used as for the deployed instance but in a different "setup" so it uses dandi-api

- https://gui-beta-dandiarchive-org.netlify.app/ is the deployed Web UI instance working against dandi-api 

### https://github.com/dandi/dandi-api/ - DANDI API service/backend

is DJANGO-based implementation of the DANDI API service to which both web UI 
(https://github.com/dandi/dandiarchive)

- https://api.dandiarchive.org/swagger/ provides swagger interface to see and play around with the API server

### https://github.com/dandi/dandi-cli/ - CLI/Python client

The same client, but with `DANDI_DEVEL=1` env variable would enable command line options to interact with 
`dandi-api` instead of a deployed instance.

### https://github.com/dandi/schema - exported DANDI schema

Contains json schemas for DANDI metata schema defined and exported by/from https://github.com/dandi/dandi-cli/ where 
it resides in https://github.com/dandi/dandi-cli/blob/master/dandi/models.py and https://github.com/dandi/dandi-cli/blob/master/dandi/model_types.py


### http://github.com/dandi/dandi-api-datasets - CI dataset for metadata conversion & validation

Automatically updated (on drogon) given the current state of dandisets in the archive and dandi-cli (schema etc)