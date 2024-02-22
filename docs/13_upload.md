# Create Dandisets and Upload Data

You can create a new Dandiset at [http://dandiarchive.org](http://dandiarchive.org). 
This Dandiset can be fully public or embargoed according to NIH policy.
When you create a Dandiset, a permanent ID is automatically assigned to it.

To prevent the production server from being inundated with test Dandisets, we encourage developers to develop 
against the development server ([https://gui-staging.dandiarchive.org/](https://gui-staging.dandiarchive.org/)). Note 
that the development server
should not be used to stage your data. All data are uploaded as draft and can be adjusted before publishing on
the production server. The development server is primarily used by users learning to use DANDI or by developers.

The below instructions will alert you to where the commands for interacting with these 
two different servers differ slightly. 

## Install DANDI Client

1. To create a new Dandiset and upload your data, you need to have a DANDI account.  See [Create a DANDI Account](./16_account.md).
1. Log in to DANDI and copy your API key. Click on your user initials in the
    top-right corner after logging in. Production (dandiarchive.org) and staging (gui-staging.dandiarchive.org) servers 
      have different API keys and different logins.
1. Locally:
    1. Create a Python environment. This is not required, but strongly recommended; e.g. [miniconda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html),
         [virtualenv](https://docs.python.org/3/library/venv.html).
    2. Install the DANDI CLI into your Python environment:

            pip install -U dandi

    3. Store your API key somewhere that the CLI can find it; see ["Storing
          Access Credentials"](#store-access-credentials) below.

## Store Access Credentials

There are three options for storing your DANDI access credentials.

1. `DANDI_API_KEY` Environment Variable

    - By default, the DANDI CLI looks for an API key in the `DANDI_API_KEY`
      environment variable.  To set this on Linux or macOS, run:

            export DANDI_API_KEY=personal-key-value

    - Note that there are no spaces around the "=".

1. `keyring` Library
    - If the `DANDI_API_KEY` environment variable is not set, the CLI will look up the API
      key using the [keyring](https://github.com/jaraco/keyring) library, which
      supports numerous backends, including the system keyring, an encrypted keyfile,
      and a plaintext (unencrypted) keyfile.

    - You can store your API key where the `keyring` library can find it by using
      the `keyring` program: Run `keyring set dandi-api-dandi key` and enter the
      API key when asked for the password for `key` in `dandi-api-dandi`.

    - You can set the backend the `keyring` library uses either by setting the
      `PYTHON_KEYRING_BACKEND` environment variable or by filling in [the `keyring`
      library's configuration file](https://github.com/jaraco/keyring#configuring).
      IDs for the available backends can be listed by running `keyring --list`.  If
      no backend is specified in this way, the library will use the available
      backend with the highest priority.

1. Manual Password Entry
    - If the API key isn't stored in either the `DANDI_API_KEY` environment variable
      or in the keyring, the CLI will prompt you to enter the API key, and then it
      will store it in the keyring.  This may cause you to be prompted further; you
      may be asked to enter a password to encrypt/decrypt the keyring, or you may be
      asked by your OS to confirm whether to give the DANDI CLI access to the
      keyring.

    - If the DANDI CLI encounters an error while attempting to fetch the API key
      from the default keyring backend, it will fall back to using an encrypted
      keyfile (the `keyrings.alt.file.EncryptedKeyring` backend).  If the keyfile
      does not already exist, the CLI will ask you for confirmation; if you answer
      "yes," the `keyring` configuration file (if it does not already exist; see
      above) will be configured to use `EncryptedKeyring` as the default backend.
      If you answer "no," the CLI will exit with an error, and you must store the
      API key somewhere accessible to the CLI on your own.

## Register a Dandiset

Register a Dandiset to generate an identifier. 

1. After logging in on https://dandiarchive.org, click the `NEW DANDISET` button in the top right corner. 
1. You will be asked to enter basic metadata for your dataset:
    1. Title (i.e. name)
    1. Description (i.e. abstract)
    1. License
1. The dataset identifier will be created; we will call this `<dataset_id>`.

## Standardize your dataset

The data within Dandisets should be standardized to the NWB, and/or BIDS data standards.
Standardize with NWB files (and optionally with the BIDS standard), if your dataset includes electrophysiology, optical physiology, tracking, or stimlus data.
Standardize with the BIDS standard, if your dataset includes MRI or microscopy data.
Below are instructions on how to organize your data into these standards, and create your Dandiset.

1. NWB dataset or BIDS dataset with NWB files
    1. Convert your data to NWB 2.1+ in a local folder. Let's call this `<source_folder>`.
    We suggest beginning the conversion process using only a small amount of data so that common issues may be spotted earlier in the process.
    This step can be complex depending on your data.
    [NeuroConv](https://neuroconv.readthedocs.io/) automates
    conversion to NWB from a variety of popular formats.
	[nwb-overview.readthedocs.io](https://nwb-overview.readthedocs.io)
    points to more tools helpful for working with NWB files, and [BIDS
    converters](https://bids.neuroimaging.io/benefits.html#converters)
    if you are preparing a BIDS dataset containing NWB files.
    Feel free to [reach out to us for help](https://github.com/dandi/helpdesk/discussions).

    1. Check your files for [NWB Best Practices](https://nwbinspector.readthedocs.io/en/dev/best_practices/best_practices_index.html) by installing
    the [NWBInspector](https://nwbinspector.readthedocs.io/en/dev/user_guide/user_guide_index.html) (`pip install -U nwbinspector`) and running

                nwbinspector <source_folder> --config dandi

    1. Thoroughly read the NWBInspector report and try to address as many issues as possible. **DANDI will prevent validation and upload of any issues
    labeled as level 'CRITICAL' or above when using the `--config dandi` option.**
    See 
       ["Validation Levels for NWB Files"](./135_validate.md) for more information about validation criteria for 
       uploading NWB 
       files and which are deemed critical. We recommend regularly running the inspector early in the process to generate the best NWB files possible. 
    Note that some autodetected violations, such as `check_data_orientation`, may be safely ignored in the event 
       that the data is confirmed to be in the correct form; this can be done using either the `--ignore <name_of_check_to_suppress>` flag or a config file. See [the NWBInspector CLI documentation](https://nwbinspector.readthedocs.io/en/dev/user_guide/using_the_command_line_interface.html) for more details and other options, or type `nwbinspector --help`.
    If the report is too large to efficiently navigate in your console, you can save a report using

            nwbinspector <source_folder> --config dandi --report-file-path <report_location>.txt

    1. Once your files are confirmed to adhere to the Best Practices, perform an official validation of the NWB files by running:

            dandi validate --ignore DANDI.NO_DANDISET_FOUND <source_folder>
        
        - If you are having trouble with validation, make sure the conversions were run with the most recent version of `dandi`, `PyNWB` and `MatNWB`.**

    1. Now, prepare the Dandiset folder used for upload:

            dandi download https://dandiarchive.org/dandiset/<dataset_id>/draft
            cd <dataset_id>
            dandi organize <source_folder> -f dry
            dandi organize <source_folder>

        - The `dandi organize` steps should not be used if you are preparing a BIDS dataset with the NWB files.
        - Renaming files with `dandi organize` can be customized with the [--required-field](https://dandi.readthedocs.io/en/latest/cmdline/organize.html#cmdoption-required-field) option.
        - If you have an issue using the `dandi` CLI, see the [Dandi Debugging section](./15_debug.md).

1. BIDS dataset
    1. Convert your data to BIDS standard in a local folder. Let's call this `<source_folder>`.
    We suggest beginning the conversion process using only a small amount of data so that common issues may be spotted earlier in the process.
    This step can be complex depending on your data.
    [BIDS converters](https://bids.neuroimaging.io/benefits.html#converters)
    automate conversion to BIDS from a variety of popular formats and the [BIDS specification](https://bids-specification.readthedocs.io/) provides more information on the BIDS standard.
    Feel free to [reach out to us for help](https://github.com/dandi/helpdesk/discussions).

    1. Once your files are confirmed to adhere to the BIDS standard, perform an official validation of the BIDS files using the [BIDS validator](https://github.com/bids-standard/bids-validator).

    1. Download the Dandiset folder used for upload:

            dandi download https://dandiarchive.org/dandiset/<dataset_id>/draft
            cd <dataset_id>

    1. Move your `<source_folder>/` content (i.e. BIDS dataset) into the Dandiset folder.

    1. Check your files with the BIDS Validator and try to address as many issues as possible.

            dandi validate --ignore DANDI.NO_DANDISET_FOUND <source_folder>

    1. Dandisets with Zarr assets currently cannot be versioned and published.  We are 
actively working on enabling this feature. 

## Upload data

1. Validate the Dandiset folder, and begin upload:

        dandi validate .
        dandi upload

1. Note:
    1. Upload to the development server with the `-i` option, e.g.
    `dandi upload -i dandi-staging`.
    1. Validation is also done during `upload`, but ensuring compliance using `validate` prior to upload helps avoid interruptions of the lengthier upload process due to validation failures.
    1. If you have an issue using the `dandi` CLI, see the [Debug section](./15_debug.md).

## Add Dandiset metadata

1. Add metadata by visiting your Dandiset landing page at
  `https://dandiarchive.org/dandiset/<dataset_id>/draft` and clicking on the `METADATA` link.
