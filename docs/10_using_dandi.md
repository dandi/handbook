# Working with DANDI

DANDI provides access to and an archive to submit cellular neurophysiology 
datasets. We refer to such datasets as a `Dandiset`. 

1. A `Dandiset` is organized in a structured manner to help improve users and 
software tools can interact with it. 
1. Each `Dandiset` has a unique persistent identifier that you can use to go directly 
to the `Dandiset` (e.g., [https://identifiers.org/DANDI:000004](https://identifiers.org/DANDI:000004)).
You can use this identifier to cite the `Dandiset` in your publications or providing
direct access to a `Dandiset`.

## DANDI components

### The DANDI Web application

[DANDI Web application](https://dandiarchive.org/) allows you to:

1. Browse `Dandisets`.
1. Search across `Dandisets`. 
1. Create an account to register a new `Dandiset` or gain access to 
[the Dandihub analysis platform](#the-dandihub-analysis-platform).
1. Add collaborators to your `Dandiset`.
1. Retrieve an `API key` to perform data upload to your `Dandisets`.
1. Publish versions of your `Dandisets`.

### The DANDI Python client

The [DANDI Python client](https://pypi.org/project/dandi/) allows you to:

1. Download `Danidsets` and individual subject folders or files.
1. Organize your data locally before upload.
1. Upload your `Dandiset`

### The Dandihub analysis platform

[Dandihub](https://hub.dandiarchive.org) provides a Jupyter environment to 
interact with the DANDI archive. To use the hub, you will need to register an
account using [the DANDI Web application](#the-dandi-web-application). Please
note that `Dandihub` is not intended for significant computation, but provides a
place to introspect `Dandisets` and files.  

## Downloading from DANDI

You can download entire `Dandisets` or single files.

### Downloading a file

#### Using the Web application. 

Each `Dandiset` has a `View Data` option. This provides a folder like view to
navigate a `Dandiset`. Any file in the `Dandiset` has a download icon next to it.
You can click this icon to download a file to your device where you are browsing
or right click to get the download URL of the file. You can then use this URL 
programmatically or in other applications such as the [NWB Explorer](https://nwbexplorer.opensourcebrain.org/)
or in a [Jupyter notebook on Dandihub](https://hub.dandiarchive.org).

#### Using the Python CLI

First install the Python client using `pip install dandi` in a Python 3.6+ 
environment.

1. Downloading a `Dandiset`.
1. Downloading a subject.
1. Downloading a file.

## Create an account on DANDI

To create an account on DANDI, you will need to.

1. [Create a Github account](https://github.com/) if you don't have one.
1. Using your Github account [register a DANDI account](https://gui.dandiarchive.org/#/user/register). 
   **Make sure to use the Register with OAuth option**
1. You will receive an email acknowledging activation of your account within 24 
hours. You can now login to DANDI using the Github by clicking on the login 
button.

## Uploading a Dandiset

1. Setup
    - If you do not have a DANDI account, please [create an account](#create-an-account-on-dandi)
    - Log in to DANDI, copy your API key. This is under your user initials on the 
    top right after logging in.
    - Locally
        - Create a Python environment (e.g., Miniconda, virtualenv)
        - Install the DANDI CLI into your Python environment
         
            `pip install dandi`
 
1. Data upload/management workflow
    1. Register a dandiset to generate an identifier. You will be asked to enter 
      basic metadata, a name (title) and description (abstract) for your dataset. 
      Click `New Dataset` in the Web application after logging in. After you are 
      done, note the dataset identifer. We will call this `<dataset_id>`.
    1. Convert your data to NWB 2.1+ in a local folder. Let's call this `<source_folder>`
    This step can be complex depending on your data. Feel free to [reach out to 
    us for help](/#where-to-communicate).
    1. Validate the NWB files by running: `dandi validate <source_folder>`
    1. Preparing a dataset folder for upload:
        1. `dandi download https://dandiarchive.org/<dataset_id>/draft` 
        1. `cd <dataset_id>`
        1. `dandi organize <source_folder> -f dry`
        1. `dandi organize <source_folder> -f symlink`
        1. `dandi upload`
    1. Add metadata on the Web. Click on the `Edit metadata` link by visiting 
    your dandiset landing page: `https://dandiarchive.org/<dataset_id>/draft`
    1. Use the dandiset URL: 
        1. in your preprint
        1. To download, anyone can use the dandi CLI:
            `dandi download <dandiset_url>`

## Publish a Dandiset 

**🛠 Work in progress 🛠**

 

