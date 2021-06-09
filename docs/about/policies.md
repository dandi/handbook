# General Policies v1.0

## Content

- **Scope:** Neurophysiology research. Raw and derived experimental data. Content
  must not violate privacy or copyright, or breach confidentiality or non-disclosure
  agreements for data collected from human subjects.
- **Status of research data:** Any status is accepted, from any stage of the
  research lifecycle.
- **Eligible depositors:** Anyone may register as user of DANDI. All users are
  allowed to deposit content for which they possess the appropriate rights.
- **Ownership:** By uploading content, no change of ownership is implied and no
  property rights are transferred to the DANDI team. All uploaded content remains
  the property of the parties prior to submission.
- **Data file formats:** DANDI only accepts data using standardized formats such
  as [Neurodata Without Borders](https://nwb.org),[Brain Imaging Data Structure](https://bids.neuroimaging.io/),
  [Neuroimaging Data Model](NIDM) and other [BRAIN Initiative](https://braininitiative.nih.gov/)
  standards. We are working with the community to improve these standards and to
  improve metadata to make the datasets more FAIR.
- **Volume and size limitations:** There is a limit of 5TB per asset and we currently
  accept any size of standardized datasets, as long as you can upload them over
  an HTTP connection. However, if you plan to upload more than 50TB of data please
  get in touch with us.
- **Data quality:** All information is provided “as-is”, and the user shall hold
  DANDI and information providers supplying data to Zenodo free and harmless in
  connection with the use of such information.
- **Metadata types and sources:** All metadata is stored internally in JSON-format
  according to a defined JSON schema. Metadata is exported in several standard
  formats such as JSON-LD and DataCite Metadata Schema.
- **Language:** For textual items, English is preferred but all languages are
  accepted.
- **Licenses:** Users must specify a license for each dataset.

## Access and Reuse

- **Access to data objects:** Files may be deposited under open <!--or embargoed-->
  access. Access to metadata and data files is provided over standard protocols
  such as HTTP.
- **Use and re-use of data objects:** Use and re-use is subject to the license
  under which the data objects were deposited.
- **Metadata access and reuse:** Metadata is licensed under CC0, except for email
  addresses. All metadata is exported via HTTP and can be harvested.

<!--
- **Embargo status:** Users may deposit content under an embargo status and
  provide an anticipated end date for the embargo. The repository will restrict
  access to the data until the end of the embargo period; at which time, the
  content will become publically available automatically. The end of the embargo
  period is the earliest of the date provided by submitter, the first publication
  using the data, or the end of funding support for the collection and/or disemmination
  of the dataset.
- **Restricted Access:** Depositors of embargoed datasets have the ability to
  share access with other collaborators. These files will not be made publicly
  available till the end of the embargo period.
-->

## Removal

- **Revocation:** Content not considered to fall under the scope of the repository
  will be removed and associated DOIs issued by DANDI revoked. Please signal
  promptly, ideally no later than 24 hours from upload, any suspected policy
  violation. Alternatively, content found to already have an external DOI will
  have the DANDI DOI invalidated and the record updated to indicate the original
  external DOI. User access may be revoked on violation of Terms of Use.
<!--
Enable after publish is in place
- **Withdrawal:** If the uploaded research object must later be withdrawn, the
  reason for the withdrawal will be indicated on a tombstone page, which will
  henceforth be served in its place. Withdrawal is considered an exceptional
  action, which normally should be requested and fully justified by the original
  uploader. In any other circumstance reasonable attempts will be made to contact
  the original uploader to obtain consent. The DOI and the URL of the original
  object are retained.
-->
- **User data on Dandihub:** At present user data on Dandihub will be removed at
  periodic intervals and should not be seen as persistent.

## Longevity

- **Versions:** Datasets are versioned when published. Prior to publishing the
  state of a dataset may continue to evolve and the data or metadata are not
  versioned. Derivatives of data files may be generated, but original content is
  never modified.
- **Replicas:** All data files are stored on an AWS public bucket, with replicas
  housed at Dartmouth College.  Data files are kept in multiple replicas at the
  moment, but this may change over time.
- **Retention period:** Items will be retained for the lifetime of the repository.
  This is currently the lifetime of the NIH award, which currently expires in
  April 2024.
- **Functional preservation:** DANDI makes no promises of usability and
  understandability of deposited objects over time.
- **File preservation:** Data files and metadata are backed up nightly and
  replicated into multiple copies in the online system.
- **Fixity and authenticity:** All data files are stored along with multiple
  checksum of the file content. Files are regularly checked against their
  checksums to assure that file content remains constant.
- **Succession plans:** In case of closure of the repository, best efforts will
  be made to integrate all content into suitable alternative institutional and/or
  subject based repositories.

This policy document is derived from the [Zenodo General Policies v1.0](https://about.zenodo.org/policies/).
