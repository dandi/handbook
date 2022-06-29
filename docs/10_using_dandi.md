# Using DANDI

The DANDI project can be represented schematically by the figure:

<img
src="../img/dandi_structure.svg"
alt="dandi_structure"
style="width: 70%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>

The Clients are DANDI Python CLI and DANDI Web application and the Server side contains a RESTful API and DANDI JupyterHub. The file organization to store data together with metadata is called `Dandiset`.

## Dandisets

DANDI stores cellular neurophysiology datasets. We refer to such datasets as `Dandisets`.

Formally, a `Dandiset` is a collection of assets (files and their metadata) and metadata about the collection.

1. A `Dandiset` is organized in a structured manner to help users and
software tools interact with it.
1. Each `Dandiset` has a unique persistent identifier that you can use to go directly
to the `Dandiset` (e.g. [https://identifiers.org/DANDI:000004](https://identifiers.org/DANDI:000004)).
You can use this identifier to cite the `Dandiset` in your publications or provide
direct access to a `Dandiset`.

### **Dandiset actions**

Anyone on the Internet can view and download public `Dandisets`. Registered users can also create `Dandisets`, upload data, and publish the `Dandiset` to generate a DOI for it.

<img
src="../img/dandiset_activity.svg"
alt="dandiset_activity"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>


You can learn more about the `Dandiset` actions in separate sections:

- [View](./11_view.md)
- [Download](./12_download.md)
- [Upload](./13_upload.md)
- [Publish](./14_publish.md)


## DANDI Components

### **The DANDI Web application**

The [DANDI Web application](https://dandiarchive.org/) allows you to:

* Search across all public `Dandisets`
* Download data from public `Dandisets`
* Create a new `Dandiset` and provide metadata
* Publish your `Dandiset`


### **The DANDI Python client**

The [DANDI Python client](https://pypi.org/project/dandi/) allows you to:

* Download `Danidsets` and individual subject folders or files
* Organize your data locally before upload
* Upload `Dandisets`

Before you can use the DANDI Python client, you have to install the package with `pip install dandi` in a Python 3.7+
environment.

You should check the [Dandi Debugging section](./15_debugging.md) in case of any problems.

### **The Dandihub analysis platform**

[Dandihub](https://hub.dandiarchive.org) provides:
- a JupyterHub instance in the cloud to interact with the data stored in DANDI.

To use the hub, you will need to register for an
account using the [DANDI Web application](https://dandiarchive.org/). 
Note that `Dandihub` is not intended for significant computation, but provides a place to introspect `Dandisets` and to perform some analysis and visualization of data.

