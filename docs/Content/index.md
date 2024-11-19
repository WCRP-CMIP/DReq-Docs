# DReq Content: technical details

The information used by the data request is version controlled [here](https://github.com/CMIP-Data-Request/CMIP7_DReq_Content).
This information is referred to as the data request "content".
It includes all information linking scientific goals to the output variables requested from particular CMIP experiments, and the CF metadata required to completely characterize the output variables.
The content is versioned separately from the [data request software](https://github.com/CMIP-Data-Request/CMIP7_DReq_Software), which provides an interface to query and utilize the content. 
**Users should not interact with the content files directly**, as the software is intended for this purpose.

Airtable databases ("bases") maintained by the CMIP IPO and Data Request Task Team are the primary source of the content.
These Airtable bases are used to manage the information gathered by the extensive community consultation undertaken to develop the CMIP7 data request.
The content repository stores exports of the information from Airtable in `json` files.
Although `json` files are easily viewable in any text editor, the format of these exported content files is not designed for readability since users should interact with data request content either by using the software or by navigating the Airtable online interface.

While users should not interact directly with the expored content files, for reference we document here some basic aspects of these files.
There are two flavours of exported content file:

- `dreq_release_export.json` contains the content of an official data request release. New versions of this file correspond to tags in this repository with the names of official releases (e.g. `v1.0beta` or `v1.0`).

- `dreq_raw_export.json` contains the content of the "working" bases used by the Data Request Task Team, CMIP IPO, and Thematic Author Teams to develop the data request. It is updated on an ongoing basis (i.e., there can be updates between official releases). Its format differs slightly from that of `dreq_release_export.json`, but for tagged versions its information content should be consistent with `dreq_release_export.json`.

The basic structure of an export file is:
```
{
    'base name 1' : {
        'table name 1' : {
            ...
            'records' : { # dict to contain all records (rows) in the table, indexed by each record's unique id string
                record id 1 : {record info}
                record id 2 : {record info}
                ...
            },
            'fields' : { # dict to contain schema info about the fields found in each record
                field id 1 : {field info}
                field id 2 : {field info}
                ...
            },
        'table name 2' : {...}
        ...
        }
    }
    'base name 2' : {...}
    ...
}
```
For example:
```json
{
  "Data Request Opportunities (Public)": {
    "Comment": {
      "base_id": "appbrFryP1MhstOS3",
      "base_name": "Data Request Opportunities (Public)",
      "id": "tblQqiAzywOppDNvj",
      "name": "Comment",      
      "description": "",
      "fields": {
        "fld5PnZpNhaifVJ8z": {
          "description": "Comment Title",
          "name": "Comment Title",
          "type": "singleLineText"
        },
        "fldKYZsaRAapA58NG": {
          "description": "Variable groups relevant to the comment.",
          "linked_table_id": "tbl4x1RxPwKRZ0VXY",
          "name": "Variable Groups",
          "type": "multipleRecordLinks"
        }, 
    ... 
      "records": {
        "rec5E9oBVZsxdxHKN": {
          "Comment": "The reference to Omon.sltbasin (Omon.slftbasin) is wrong and must be changed to Omon.sltbasin.\n",
          "Comment Title": "Update description",
          "Opportunities": [
            "reczXng420cBQ08hg"
          ],
          "Status": "Done",
          "Theme": [
            "Ocean & Sea-Ice"
          ],
          "Variable Groups": [
            "recPohW0nDzLULHye"
          ]
        },
        ...
```

Each base is a separate top-level entry ("base" is Airtable's term for database).
This is necessary to ensure the integrity of links between different tables in each base.
They are self-consistent within a base, but not across different bases.
Note however that release versions (`dreq_release_export.json`) contain only one base.
To create release versions, tables from public views of the three "working bases" (Opportunities, Physical Parameters, and Variables) at the release time are consolidated in Airtable into a single, static self-consistent base.

In any export, links from a record to one or more other records in other tables appear as lists of record id strings.
In the above example, "Opportunities" and "Variable Groups" are both links (in this instance the lists have length = 1).
The field description indicates which table a link points to, which in the above example for "Variable Groups" is the table with the id string given by `linked_table_id`.
(In this instance it's obvious which table is linked to because the field name is the same as the table name, but that's not required and isn't always the case.)
Note that the unique ids of records, such as `"recPohW0nDzLULHye"`, or of other entities in the export (tables, fields, and bases), are **not equivalent to the persistent unique identifiers (uid) of data request objects**. 
These ids are internally generated when the information is exported from airtable, and provide self-consistent identifiers within the export file but are not persistent identifiers.

