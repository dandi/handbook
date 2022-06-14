# Downloading Data


## Using the DANDI Web application

Once you have the `Dandiset` you are interested in (see more in [the Dandiset View section](./11_view.md)), you can download the content of the `Dandiset`.
On the landing page of each `Dandiset` you can find `Download` button on the right-hand panel. After clicking the button, you will see the specific command you can use with DANDI Python CLI (as well as the information on how to download the CLI).

<p float="left">
<img
src="./img/web_dandiset_rsp_download.png"
alt="web_dandiset_rsp_download"
style="width: 30%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>
</p>

### Downloading specific files

The right side panel of the `Dandiset` landing page allows you also to access the list of folders and files.

<img
src="./img/web_dandiset_files.png"
alt="web_dandiset_files"
style="width: 60%; height: auto; display: block; margin-left: auto;  margin-right: auto;"/>


Each file in the `Dandiset` has a download icon next to it, clicking the icon will start the download process.



## Using the Python CLI

The [DANDI Python client](https://pypi.org/project/dandi/) gives you more option to download entire `Dandisets` and part of the data.

### Download a `Dandiset`
In order to download entire `Dandiset` you can use the same command as suggested by DANDI web application, e.g.: 

`dandi download DANDI:000023`

### Download data for a specific subject from a Dandiset
You can download data for the specific subjects. 
Names of the subjects could be found on DANDI web application or by running a commend with the DANDI CLI: `dandi ls -r DANDI:000023`.
Once you have the subject id, you can download the data, e.g.:

`dandi download https://api.dandiarchive.org/api/dandisets/000023/versions/draft/assets/?path=sub-811677083`

You should replace `draft` with a specific version you are interested in (e.g. `0.210914.1900` in the case of this Dandiset).

You can also use the link from DANDI web application, e.g.:

`dandi download https://dandiarchive.org/dandiset/000023/0.210914.1900/files?location=sub-541516760%2F`


### Download a specific file from a Dandiset 
Link for the specific file could be found on the DANDI web application, e.g.:

`dandi download https://api.dandiarchive.org/api/dandisets/000023/versions/0.210914.1900/assets/1a93dc97-327d-4f9c-992d-c2149e7810ae/download/`


**Hint:** `dandi download` supports a number of resource identifiers to point to Dandiset, folder, or file.  Providing 
an incorrect URL (e.g. `dandi download wrongurl`) will provide a list of supported identifiers.

**Remember, that you need to have Python 3.7+ and install the DANDI Python Client using `pip install dandi`.
In case you have an issue with using Python CLI, please visit [Dandi Debugging section](./15_debugging.md)**.