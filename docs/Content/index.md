# DReq Content: technical details

The information used by the data request is version controlled [here](https://github.com/CMIP-Data-Request/CMIP7_DReq_Content).
This information is referred to as the data request "content".
It includes all information linking scientific goals to the output variables requested from particular CMIP experiments, and the CF metadata required to completely characterize the output variables.
The content is versioned separately from the [data request software](https://github.com/CMIP-Data-Request/CMIP7_DReq_Software), which provides an interface to query and utilize the content. 
Users should not interact with the content files directly, as the software is intended for this purpose.

Airtable databases ("bases") maintained by the CMIP IPO and Data Request Task Team are the primary source of the content.
These Airtable bases are used to manage the information gathered by the extensive community consultation undertaken to develop the CMIP7 data request.
The content repository stores exports of the information from Airtable in `json` files.
Although `json` files are easily viewable in any text editor, the format of these exported content files is not designed for readability (as noted above, the software should be used to interact with the content files).

There are two flavours of exported content file:

- `dreq_release_export.json` contains the content of an official data request release. New versions of this file correspond to tags in this repository with the names of official releases (e.g. `v1.0beta`).

- `dreq_raw_export.json` contains the content of the "working" bases used by the Data Request Task Team, CMIP IPO, and Thematic Author Teams to develop the data request. It is updated on an ongoing basis (i.e., there can be updates between official releases). Its format differs slightly from that of `dreq_release_export.json`, but for tagged versions its information content should be consistent with `dreq_release_export.json`.


