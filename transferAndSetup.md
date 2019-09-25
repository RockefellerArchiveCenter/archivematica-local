---
layout: docs
title:  "RAC Archivematica | Set up for Transfer"
---


## Transfer Structure

Archivematica requires a directory structure that is compliant with Archivematica's SIP directory structure for the following types of transfers:

*  transfers with multiple versions of digitized files
*  transfer with metadata, such as an archivesspaceids.csv or rights.csv
*  transfers with manually normalized files
*  transfers with submission documentation

As these are the vast majority of our use cases, all transfers ingested into Archivematica should be in a structured directory. A structured directory includes the following subdirectories:

*  **objects**: The `/objects` directory contains the digital objects that are to be preserved. This can contain subdirectories.
*  **metadata**: The `/metadata` directory will eventually contain the checksum and the METS file. At the point of transfer, the `/metadata` directory contains the ArchivesSpace IDs CSV and the PREMIS CSV.
*  **logs**: The `/logs` directory will eventually contain logs generated when processing the transfer in Archivematica.

The following directory structure examples are for Standard Transfers, which will be used the majority of the time. Transfers can also be zipped or unzipped bags, in which case all subdirectories should be in the `/data` directory.

### Examples

#### Digitized Material

Master files are in directory "Master," master edited files are in directory "Master Edited," and serviced edited files are in directory "Service Edited." The output should look like either of the following (depending on access format):


##### Access format: concatenated PDF

<div class="docs-example code codeblock">/archivematica_sip_examplerefid
  /logs
  /metadata
    archivesspaceids.csv
    rights.csv
  /objects
    examplerefid_001.tif
    examplerefid_002.tif
    examplerefid_003.tif
    examplerefid.pdf
    /access
      examplerefid.pdf
    /service
      examplerefid_001.tif
      examplerefid_002.tif
      examplerefid_003.tif
</div>

##### Access format: JPGs

<div class="docs-example code codeblock">/archivematica_sip_examplerefid
  /logs
  /metadata
    archivesspaceids.csv
    rights.csv
  /objects
    examplerefid_001.tif
    examplerefid_002.tif
    examplerefid_003.tif
    /access
      examplerefid_001.jpg
      examplerefid_002.jpg
      examplerefid_003.jpg
    /service
      examplerefid_001.tif
      examplerefid_002.tif
      examplerefid_003.tif
</div>

#### Legacy Born Digital

##### With Manually Normalized Files

<div class="docs-example code codeblock">/top-level
  /logs
  /metadata
    archivesspaceids.csv
    rights.csv
  /objects
    digital-object1.doc
    digital-object2.pdf
    /manualNormalization
      /access
        digital-object1.docx
      /preservation
        digital-object1.docx
</div>

##### Without Manually Normalized Files
<div class="docs-example code codeblock">/top-level
  /logs
  /metadata
    archivesspaceids.csv
    rights.csv
  /objects
    digital-object1.pdf
    digital-object2.pdf
    digital-object3.docx
</div>

## Transfer Metadata

Generally, two metadata files are included in RAC transfers. These are:

* `archivesspaceids.csv`: This file contains information to automatically match descriptive information in ArchivesSpace to access objects that are in the Archivematica DIP.
* `rights.csv`: This file contains PREMIS rights information that is included in the METS file in the AIP. This information is also used in the ArchivesSpace DIP upload integration.

### ArchivesSpace IDs CSV

In order to automatically match access files with components in ArchivesSpace, a CSV file with the filename `archivesspaceids.csv` must be included in the `/metadata` directory in the transfer. The first column contains the filenames and the second column contains the refid of the component the file needs to be linked to. There is no header row.

Note that filenames, including file extensions, are case sensitive, and should contain the full path either including or after the `/objects` directory. If a manually normalized access version of the file is included in the transfer, the filepath to include in the first column should be the access version; if an access version is not included, the filepath in the first column should be for the original object. For digitized transfers with `/access` and `/service` directories, the filepath should be to the original object. For digitized transfers where the access copy is a multi-page pdf but the preservation copies are multiple tif files, the filepath should be for the pdf file(s) only, but for the pdf file(s) that sit in the `/objects` directory.

*No access version:*

| objects/Youth Organizations.doc | ref5086\_rts |
| objects/Meeting Minutes.pdf | ref5086\_rts |
| objects/Youth Organizations Revised.doc | ref5086\_rts |

*Manually normailzed born digital with access version*

| objects/manualNormalization/access/Youth Organizations.docx | examplerefid |
| objects/manualNormalization/access/Meeting Minutes.pdf | examplerefid |
| objects/manualNormalization/access/Youth Organizations Revised.docx | examplerefid |

*Digitized with jpg access copies*

| objects/examplerefid_001.tif | examplerefid |
| objects/examplerefid_002.tif | examplerefid |
| objects/examplerefid_003.tif | examplerefid |

*Digitized with pdf access copy*

| objects/access/examplerefid.pdf | examplerefid |

### PREMIS CSV

PREMIS rights information is included in the METS file in the AIP and is used to write information to ArchivesSpace as part of the ArchivesSpace DIP Upload Integration. For details on how PREMIS rights information is mapped to ArchivesSpace, see the [Appendix](appendix#premis-mapping). In order to include rights information with the transfer, a `rights.csv` file must be included in the `/metadata` directory of the transfer. For digitized transfers, the rights.csv should include files in the `/objects` directory, including (if applicable) the multipage pdf file.

*Example:*

<div class="table-responsive" markdown="block">

| file | basis | status | determination_date | jurisdiction | start_date | end_date | terms | citation | note | grant_act | grant_restriction | grant_start_date | grant_end_date | grant_note | doc_id_type | doc_id_value | doc_id_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| r2fp9q4b_004.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open | | | Copyright note | publish | Allow | 1/1/00 | open | Grant note | | | |
| r2fp9q4b_004.tif | donor | | | | 1/1/90 | open | | | Donor note | disseminate | Allow | 1/1/90 | open | Grant note | | | |
| r2fp9q4b_001.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open | | | Copyright note | publish | Allow | 1/1/00 | open | Grant note | | | |
| r2fp9q4b_001.tif | donor | | | | 1/1/90 | open | | | Donor note | disseminate | Allow | 1/1/90 | open | Grant note | | | |
| r2fp9q4b_002.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open | | | Copyright note | publish | Allow | 1/1/00 | open | Grant note | | | |
| r2fp9q4b_002.tif | donor | | | | 1/1/90 | open | | | Donor note | disseminate | Allow | 1/1/90 | open | Grant note | | | |
| r2fp9q4b_003.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open | | | Copyright note | publish | Allow | 1/1/00 | open | Grant note | | | |
| r2fp9q4b_003.tif | donor | | | | 1/1/90 | open | | | Donor note | disseminate | Allow | 1/1/90 | open | Grant note | | | |

</div>

## Processing Configuration

The processing configuration administration page of the dashboard allows users to configure the job decision points presented by Archivematica during transfer and ingest. This is set in the [administration tab](administration#processing-configuration). A processing congfiguration file can be included with a transfer that is ingested either via the Dashboard or the automated pipeline; if included, it will override the configuration set as the "default" in the dashboard. To create a processing configuration file, download the processing configuration from the Dashboard, and include it as `processingMCP.xml` in the top-level directory of the transfer.

## Transfer Source

Transfers must be placed in the [Transfer Source](administration#locations) in order to be ingested (either manually or automatically) into Archivematica. More information on the Transfer Source can be found in the Storage Service documentation.
