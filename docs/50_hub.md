# Using the DANDI Hub

The DANDI Hub is a JupyterHub instance in the cloud to interact with the data stored in DANDI, and is free to use for exploratory analysis of data on DANDI. Note that DANDI Hub is not intended for significant computation, but provides a place to introspect Dandisets and to perform some analysis and visualization of data.

## Registration

To use the [DANDI Hub](http://hub.dandiarchive.org), you must first register for an account using the [DANDI website](http://dandiarchive.org).

## Choosing a server option

When you start up the DANDI Hub, you will be asked to select across a number of server options. For basic exploration, Tiny or Base would most likely be appropriate. The DANDI Hub also currently offers Medium and Large options, which have more available memory and compute power. The "T4 GPU inference" server comes with an associated T4 GPU, and is intended to be used for applications that require GPU for inference. We request that users of this server be considerate of their usage of the DANDI Hub as a free community resource. Training large deep neural networks is not appropriate. A "Base (MATLAB)" server is also available, which provides a MATLAB cloud installation.

## Example notebooks

The best way to share analyses on DANDI data is through the DANDI example notebooks. These notebooks are organized by `<DANDI id>/<group>/<analysis>/<notebook.ipynb>`. Dandiset contributors are encouraged to use these notebooks to demonstrate how to read, analyze, and visualize the data, and how to produce figures from associated scientific publications.

### Contributing an example notebook

Notebooks can be submitted as a Pull Request to the [DANDI example-notebooks repository](https://github.com/catalystneuro/example-notebooks).

#### Environment specification
Best practice is to include one or more notebooks alongside an environment.yml file, which provides a conda-style specification of the environment required to run the notebooks.
1. Create a new environment: `conda create -n <env-name> -python <python-version>`
2. Use `conda install <pkg>` and `pip install <pkg>` to install the necessary dependencies until the notebook runs through successfully.
3. Export the environment: `conda env export > environment.yml`.

See detailed instructions for creating a `environment.yml` file [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#sharing-an-environment).

#### File organization
When constructing the Pull Request, ensure that you have the proper directory structure: `<DANDI id>/<group>/<analysis>/<notebook.ipynb>`. If you share more than one notebook, also include a `README.md` file at `<DANDI id>/<group>/<analysis>/README.md` explaining the purpose of each notebook and providing context and links to relevant publications.

Once this Pull Requests is accepted, your contributed notebook will be available to all DANDI Hub users.