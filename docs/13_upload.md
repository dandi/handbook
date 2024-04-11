# Creating Dandisets and Uploading Data

To create a new Dandiset and upload your data, you need to have a DANDI account.

## Create a Dandiset and Add Data

You can create a new Dandiset at https://dandiarchive.org. This Dandiset can be fully 
public or embargoed 
according to NIH policy.
When you create a Dandiset, a permanent ID is automatically assigned to it.
To prevent the production server from being inundated with test Dandisets, we encourage developers to develop 
against the development server (https://gui-staging.dandiarchive.org/). Note 
that the development server
should not be used to stage your data. All data are uploaded as draft and can be adjusted before publishing on
the production server. The development server is primarily used by users learning to use DANDI or by developers.

The below instructions will alert you to where the commands for interacting with these 
two different servers differ slightly. 

### **Setup**

1. To create a new Dandiset and upload your data, you need to have a DANDI account. See the [Create a DANDI Account](./16_account.md) page.
1. Log in to DANDI and copy your API key. Click on your user initials in the
    top-right corner after logging in. Production (dandiarchive.org) and staging (gui-staging.dandiarchive.org) servers 
      have different API keys and different logins.
1. Locally:
    1. Create a Python environment. This is not required, but strongly recommended; e.g. [miniconda](https://conda.
          io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands),
         [virtualenv](https://docs.python.org/3/library/venv.html).
    2. Install the DANDI CLI into your Python environment:

            pip install -U dandi

    3. Store your API key somewhere that the CLI can find it; see ["Storing
          Access Credentials"](#storing-access-credentials) below.

### **Data upload/management workflow**

1. Register a Dandiset to generate an identifier. You will be asked to enter
    basic metadata: a name (title) and description (abstract) for your dataset.
    Click `NEW DANDISET` in the Web application (top right corner) after logging in. 
    After you provide a name and description, the dataset identifier will be created; 
    we will call this `<dataset_id>`.
1. NWB format:
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
    2. Check your files for [NWB Best Practices](https://nwbinspector.readthedocs.io/en/dev/best_practices/best_practices_index.html) by installing
    the [NWBInspector](https://nwbinspector.readthedocs.io/en/dev/user_guide/user_guide_index.html) (`pip install -U nwbinspector`) and running

                nwbinspector <source_folder> --config dandi

    3. Thoroughly read the NWBInspector report and try to address as many issues as possible. **DANDI will prevent validation and upload of any issues
    labeled as level 'CRITICAL' or above when using the `--config dandi` option.**
    See 
       ["Validation Levels for NWB Files"](./135_validation.md) for more information about validation criteria for 
       uploading NWB 
       files and which are deemed critical. We recommend regularly running the inspector early in the process to generate the best NWB files possible. 
    Note that some autodetected violations, such as `check_data_orientation`, may be safely ignored in the event 
       that the data is confirmed to be in the correct form; this can be done using either the `--ignore <name_of_check_to_suppress>` flag or a config file. See [the NWBInspector CLI documentation](https://nwbinspector.readthedocs.io/en/dev/user_guide/using_the_command_line_interface.html) for more details and other options, or type `nwbinspector --help`.
    If the report is too large to efficiently navigate in your console, you can save a report using

            nwbinspector <source_folder> --config dandi --report-file-path <report_location>.txt

    4. Once your files are confirmed to adhere to the Best Practices, perform an official validation of the NWB files by running: `dandi validate --ignore DANDI.NO_DANDISET_FOUND <source_folder>`.
        **If you are having trouble with validation, make sure the conversions were run with the most recent version of `dandi`, `PyNWB` and `MatNWB`.**
    5. Now, prepare and fully validate again within the dandiset folder used for upload:

            dandi download https://dandiarchive.org/dandiset/<dataset_id>/draft
            cd <dataset_id>
            dandi organize <source_folder> -f dry
            dandi organize <source_folder>
            dandi validate .
            dandi upload

    Note that the `organize` steps should not be used if you are preparing a BIDS dataset with the NWB files.
    Uploading to the development server is controlled via `-i` option, e.g.
    `dandi upload -i dandi-staging`.
    Note that validation is also done during `upload`, but ensuring compliance using `validate` prior upload helps avoid interruptions of the lengthier upload process due to validation failures.
    6. Add metadata by visiting your Dandiset landing page:
       `https://dandiarchive.org/dandiset/<dataset_id>/draft` and clicking on the `METADATA` link.

If you have an issue using the Python CLI, see the [Dandi Debugging section](./15_debugging.md).

## Storing Access Credentials

There are two options for storing your DANDI access credentials.

1. `DANDI_API_KEY` Environment Variable

    - By default, the DANDI CLI looks for an API key in the `DANDI_API_KEY`
      environment variable.  To set this on Linux or macOS, run:

            export DANDI_API_KEY=personal-key-value

    - Note that there are no spaces around the "=".

2. `keyring` Library
    - If the `DANDI_API_KEY` environment variable is not set, the CLI will look up the API
        key using the [keyring](https://github.com/jaraco/keyring) library, which
        supports numerous backends, including the system keyring, an encrypted keyfile,
        and a plaintext (unencrypted) keyfile.

    - Specifying the `keyring` backend
        - You can set the backend the `keyring` library uses either by setting the
          `PYTHON_KEYRING_BACKEND` environment variable or by filling in the `keyring`
          library's [configuration file](https://github.com/jaraco/keyring#configuring).
        - IDs for the available backends can be listed by running `keyring --list`.
        - If no backend is specified in this way, the library will use the available
          backend with the highest priority.
        - If the DANDI CLI encounters an error while attempting to fetch the API key
          from the default keyring backend, it will fall back to using an encrypted
          keyfile (the `keyrings.alt.file.EncryptedKeyring` backend).  If the keyfile
          does not already exist, the CLI will ask you for confirmation; if you answer
          "yes," the `keyring` configuration file (if it does not already exist; see
          above) will be configured to use `EncryptedKeyring` as the default backend.
          If you answer "no," the CLI will exit with an error, and you must store the
          API key somewhere accessible to the CLI on your own.

    - Storing the API key with `keyring`
        1. You can store your API key where the `keyring` library can find it by using
          the `keyring` program: Run `keyring set dandi-api-dandi key` and enter the
          API key when asked for the password for `key` in `dandi-api-dandi`.

        2. If the API key isn't stored in either the `DANDI_API_KEY` environment variable
          or in the keyring, the CLI will prompt you to enter the API key, and then it
          will store it in the keyring.  This may cause you to be prompted further; you
          may be asked to enter a password to encrypt/decrypt the keyring, or you may be
          asked by your operating system to confirm whether to give the DANDI CLI access to the
          keyring.
