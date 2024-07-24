# Work In Progress -- This page should not be referenced until further abstraction is handled for the DANDI CLI tool

For data management (predominately `upload` and `download` of data 
to/from DANDI), a local CLI (command line interface) is used.

**Note: please make sure [you have set up your PyPI account](..60_initialize_vendors/##pypi).**

## Referencing your API

To reference your DANDI-clone API, [update the URLs reference per each CLI action](https://github.com/dandi/dandi-cli/blob/15196a93310618f8897c7b43444e216bbb094549/dandi/consts.py#L119-L135)

For example:

```python
known_instances = {
    "dandi": DandiInstance(
        "dandi",
        "https://<your-domain>.org",  # UI URL
        "https://api.<your-domain>.org/api", # API URL
    ),
    "dandi-staging": DandiInstance(
        "dandi-staging",
        "https://gui-staging.<your-domain>.org",
        "https://api-staging.<your-domain>.org/api",
    ),
    "dandi-api-local-docker-tests": DandiInstance(
        "dandi-api-local-docker-tests",
        f"http://{instancehost}:8085",
        f"http://{instancehost}:8000/api",
    ),
}
```

## Connecting to PyPI


## Handling Versioning




