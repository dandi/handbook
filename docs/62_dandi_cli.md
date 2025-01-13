For data management (predominately `upload`, `download` and `validation` of data 
to/from DANDI), a local CLI (command line interface) is used.

## Referencing your API

To reference your DANDI-clone API, [update the URLs reference per each CLI action](https://github.com/dandi/dandi-cli/blob/15196a93310618f8897c7b43444e216bbb094549/dandi/consts.py#L119-L135) and push a PR to the [dandi-cli GitHub repository](https://github.com/dandi/dandi-cli).

Here is an example PR of another clone adding to the available instances of `DandiInstance` objects in `dandi-cli`: [see here](https://github.com/dandi/dandi-cli/pull/1527)

For example:

```python
known_instances = {
    "dandi": DandiInstance(
        "dandi",
        "https://dandiarchive.org",
        "https://api.dandiarchive.org/api",
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
    "<your-dandi-clone>": DandiInstance( # Your own "dandi""
        "<your-dandi-clone>", # Your own "dandi"
        "https://<your-dandi-clone-domain>.org", 
        "https://api.<your-dandi-clone-domain>.org/api", 
    ),
}
```

Once your DANDI clone is added to list of available `DandiInstance` objects, you should be able to perform operations via the `-i` flag -- for example:

`dandi upload -i <your-dandi-clone>`

**Note**: Users will be prompted for a `DANDI_API_KEY`
env. var [see here for code reference](https://github.com/dandi/dandi-cli/blob/6aa414c4db47394970f586cc4fb9758a634aef87/dandi/dandiapi.py#L492-L499)

You do not need to create a unique value here -- a user can just reference the `DANDI_API_KEY` their API issues in their respective clone.

## Handling Versioning

DANDI CLI leverages a tool called [versioneer](https://pypi.org/project/versioneer/) for semantic versioning in PyPI.

Upon merging of a PR into `main`, if a given GitHub label is attached to the PR (`major`, `minor` or `patch` specifically)
`versioneer` will generate a human-readable CHANGELOG entry, and then push to PyPI the proper new semantic version.






