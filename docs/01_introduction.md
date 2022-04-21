# Introduction

## What is DANDI?

DANDI is:

- An open data archive to submit neurophysiology data for electrophysiology,
optophysiology, and behavioral time-series, and images from immunostaining experiments
- A persistent, versioned, and growing collection of standardized datasets
- A place to house data to collaborate across research sites
- Supported by the BRAIN Initiative and the AWS Public dataset programs

DANDI provides significant benefits:

- Rich metadata to support search across data
- Consistent and transparent data standards to simplify software development


## The Challenges

- To know which data are useful, data has to be accessible.
- Non-standardized datasets lead to significant resources needed to understand
and adapt code to these datasets.
- The multitude of different hardware platforms and custom binary formats requires significant
effort to consolidate into reusable datasets.
- There are many domain general places to house data (e.g. Open Science Framework,
G-Node, Dropbox, Google drive), but it is difficult to find relevant datasets.
- Datasets are growing larger requiring compute services to be closer to data.
- Neurotechnology is evolving and requires flexible extensions to metadata and
data storage requirements.
- Consolidating and creating robust algorithms (e.g. spike sorting) requires
varied data sources.

## Our Solution

We have developed a [FAIR (Findable, Accessible, Interoperable, Reusable)](https://www.force11.org/group/fairgroup/fairprinciples)
data archive to house standardized neurophysiology and associated data.
We use the [Neurodata Without Borders](https://nwb.org),
[Brain Imaging Data Structure](https://bids.neuroimaging.io/),
[Neuroimaging Data Model (NIDM)](http://nidm.nidash.org/), and other [BRAIN Initiative](https://braininitiative.nih.
gov/)
standards to organize and search the data. A JupyterHub-based analysis platform
provides easy access to the data. The data can be accessed programmatically
allowing for new software and tools to be built. The archive itself is built on
a software stack of open source products, thus enriching the ecosystem.

The archive provides persistent identifiers for versioned datasets, thus improving
reproducibility of neurophysiology research.
