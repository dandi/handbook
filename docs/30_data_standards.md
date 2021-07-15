## Data standards
DANDI requires uploaded data to adhere to community data standards. 
These standards help data curators package all of the necessary metadata, and provide a uniform
structure so that data can be more easily understood and reused by future users. 
DANDI also leverages these standards to provide features like data validation and 
automatic metadata extraction and search. DANDI currently supports two data standards: 
* For cellular neurophysiology, such as electrophysiology and optical physiology, use [Neurodata Without Borders (NWB)](https://www.nwb.org/nwb-neurophysiology/)
* For neuroimaging data, such as fMRI and PET, use [Brain Imaging Data Structure (BIDS)](https://bids.neuroimaging.io/)

To share data on DANDI, you will first need to convert your data to the 
appropriate standard. If you would like help determining which standard is most appropriate for 
your data, please do not hesitate to reach out using the
[dandi helpdesk](https://github.com/dandi/helpdesk/discussions/new)
and we would be happy to assist.

### Neurodata Without Borders (NWB)
[NWB](https://www.nwb.org/nwb-neurophysiology/) is a data standard for neurophysiology, providing 
neuroscientists with a common standard to share, archive, use, and build analysis tools for neurophysiology 
data. NWB is designed to store a variety of neurophysiology data, including data from intracellular 
and extracellular electrophysiology experiments, data from optical physiology experiments, and tracking 
and stimulus data. The NWB team supports APIs in Python ([PyNWB](https://pynwb.readthedocs.io/)) and MATLAB ([MatNWB](https://github.com/NeurodataWithoutBorders/matnwb)), with tutorials for 
writing data broken down by experiment type. See the [NWB Tutorials](https://www.nwb.org/how-to-use/) page for more details.
Also see the [NWB Conversion Tools user guide for converting data](https://nwb-conversion-tools.readthedocs.io/en/master/user_guide.html)
for automated conversions from several popular proprietary data formats. 
The best way to get help from the NWB community is through the [NWB user Slack channel](https://nwb-users.slack.com/).

### Brain Imaging Data Format (BIDS)
[BIDS](https://bids.neuroimaging.io/) is a way to organize and describe neuroimaging and behavioral data. 
See their [Getting Started page](https://bids.neuroimaging.io/getting_started.html) for instructions for how
to convert your neuroimaging data to BIDS.
