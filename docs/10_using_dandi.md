# Using DANDI


## Dandisets

DANDI provides access to an archive that stores cellular neurophysiology
datasets. We refer to such datasets as `Dandisets`.

1. A `Dandiset` is organized in a structured manner to help users and
software tools interact with it.
1. Each `Dandiset` has a unique persistent identifier that you can use to go directly
to the `Dandiset` (e.g. [https://identifiers.org/DANDI:000004](https://identifiers.org/DANDI:000004)).
You can use this identifier to cite the `Dandiset` in your publications or provide
direct access to a `Dandiset`.

### **Dandiset actions**

Everyone can view and download public `Dandisets`. 
If you are an owner of dataset, you can create a new `Dandiset` and upload the data, you can also publish teh `Dandiset`.

You can learn more about the `Dandiset` acctions in separate sections:

- [Dandisets View](./11_view.md)
- [Dandisets Download](./12_download.md)
- [Dandisets Upload](./13_upload.md)
- [Dandisets Publish](./14_publish.md)


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
- a Jupyter Hub to interact with the data stored in Dandi.

To use the hub, you will need to register an
account using the [DANDI Web application](https://dandiarchive.org/). 
Note that `Dandihub` is not intended for significant computation, but provides a place to introspect `Dandisets` and files.

