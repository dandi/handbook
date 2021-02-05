# Introduction

## Advantages of using DANDI
- An open data archive to submit cellular neurophysiology data.
- A persistent, versioned and growing collection of standardized cellular
neurophysiology data.
- Rich metadata to support search across data.
- A place to house data to collaborate across research sites.
- Consistent and transparent data standards to simplify software development.
- Supported by the BRAIN Initiative and the AWS Public dataset programs.

## The challenges

1. To know which data are useful, data has to be accessible.
1. Non standardized datasets lead to significant resources needed to understand
and adapt code to these datasets.
1. The multitude of different hardware platforms and custom binary formats requires significant
effort to consolidate into reusable datasets.
1. There are many domain general places to house data (e.g., Open Science Framework,
G-Node, Dropbox, Google drive), but it is difficult to find relevant datasets.
1. Datasets are growing larger requiring compute services to be closer to data.
1. Neurotechnology is evolving and requires flexible extensions to metadata and
data storage requirements.
1. Consolidating and creating robust algorithms (e.g., spike sorting) requires
varied data sources.

## Our solution

We have developed a [FAIR (Findable, Accessible, Interoperable, Reusable)](https://www.force11.org/group/fairgroup/fairprinciples)
data archive to house standardized cellular neurophysiology and associated data.
We use the [Neurodata Without Borders](https://nwb.org), [Brain Imaging Data Structure](BIDS),
[Neuroimaging Data Model](NIDM) and other [BRAIN Initiative](https://braininitiative.nih.gov/)
standards to organize and search the data. A Jupyterhub-based analysis platform
provides easy access to the data. The data can be accessed programmatically
allowing for new software and tools to be built. The archive itself is built on
a software stack of open source products, thus enriching the ecosystem.

The archive provides persistent identifiers for versioned datasets thus improving
reproducibility of neurophysiology research.
