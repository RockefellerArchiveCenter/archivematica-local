---
layout: docs
title:  "Set up for Transfer to Archivematica"
---


## Transfer Structure 

While Archivematica will restructure a directory for basic transfers, some transfer types require a directory structure that is compliant with Archivematica's SIP directory structure. A structured directory is required for the following types of transfers:

*  transfers with multiple versions of digitized files
*  transfer with metadata, such as an archivesspaceids.csv or rights.csv
*  transfers with manually normalized files
*  transfers with submission documention

As these are the vast majority of our use cases, all transfers ingested into Archivematica should be in a structured directory. A structured directory includes the following subdirectories:

*  **objects**: The objects directory contains the digital objects that are to be preserved. You can create subdirectories within objects if desired.
*  **metadata**: The metadata directory contains the checksum, the METS file, and a submissionDocumentation subfolder, which can be used for transfer forms, donation agreements or any other documents that relate to the acquisition of the records.
*  **logs**: The logs directory will eventually contain logs generated when processing the transfer in Archivematica.

### Digitized Material

Master files are in directory "Master," master edited files are in directory "Master Edited," and serviced edited files are in directory "Service Edited." The output should look like either of the following (depending on access format):


#### Access format: concatenated PDF

```
/archivematica_sip_examplerefid
  /logs
  /metadata
  /objects
    examplerefid_001_me.tif
    examplerefid_002_me.tif
    examplerefid_003_me.tif
    examplerefid_se.pdf
    /access
      examplerefid_se.pdf
    /service
      examplerefid_001.tif
      examplerefid_002.tif
      examplerefid_003.tif
```

#### Access format: JPGs

```
/archivematica_sip_examplerefid
  /logs
  /metadata
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
```

### Legacy Born Digital

#### With Manually Normalized Files

```
  /top-level
    /objects
      digital-object1.doc
      digital-object2.pdf
      /manualNormalization
        /access
          digital-object1.docx
        /preservation
          digital-object1.docx
    /metadata
      archivesspaceids.csv
      /submissionDocumentation
        FTKExportSummary1.txt
    /logs
```

#### Without Manually Normalized Files

```
 /top-level                                                               
   /objects                                                                 
     digital-object1.pdf                                                      
     digital-object2.pdf                                                      
     digital-object3.docx                                                     
   /metadata                                                                
     archivesspaceids.csv                                                    
     /submissionDocumentation                                                 
       FTKExportSummary1.txt                                                                                                                        
   /logs                                                                    
```

## Including Metadata in the Transfer

Generally, two metadata files are included in RAC transfers. These are:

* `archivesspaceids.csv`:
* `rights.csv`: 

### ArchivesSpace IDs CSV

In order to automatically match access files with components in 

At this stage, you can create a CSV to match files with their parent components in ArchivesSpace. There should be one CSV per SIP, with the filename "archivesspaceids.csv" in the /metadata directory. The first column contains the filenames and the second column contains the refid of the component the file needs to be linked to.There is no header row.

Note that filenames, including file extensions, are case sensitive, and should contain the full path. If files were manually normalized, the filepath should be for the original filename, not the file in the
/access directory.

For example:

| data/objects/Youth Organizations.doc  | ref5086\_rts |


### PREMIS CSV

For example:

| file | basis | status | determination_date | jurisdiction | start_date | end_date | terms | citation | note | grant_act | grant_restriction | grant_start_date | grant_end_date | grant_note | doc_id_type | doc_id_value | doc_id_role |
| access | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open |  |  | Copyright note | publish | Allow | 1/1/00 | open | Grant note |  |  |  |
| access | donor |  |  |  | 1/1/90 | open |  |  | Donor note | disseminate | Allow | 1/1/90 | open | Grant note |  |  |  |
| r2fp9q4b_004.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open |  |  | Copyright note | publish | Allow | 1/1/00 | open | Grant note |  |  |  |
| r2fp9q4b_004.tif | donor |  |  |  | 1/1/90 | open |  |  | Donor note | disseminate | Allow | 1/1/90 | open | Grant note |  |  |  |
| r2fp9q4b_001.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open |  |  | Copyright note | publish | Allow | 1/1/00 | open | Grant note |  |  |  |
| r2fp9q4b_001.tif | donor |  |  |  | 1/1/90 | open |  |  | Donor note | disseminate | Allow | 1/1/90 | open | Grant note |  |  |  |
| r2fp9q4b_002.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open |  |  | Copyright note | publish | Allow | 1/1/00 | open | Grant note |  |  |  |
| r2fp9q4b_002.tif | donor |  |  |  | 1/1/90 | open |  |  | Donor note | disseminate | Allow | 1/1/90 | open | Grant note |  |  |  |
| r2fp9q4b_003.tif | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open |  |  | Copyright note | publish | Allow | 1/1/00 | open | Grant note |  |  |  |
| r2fp9q4b_003.tif | donor |  |  |  | 1/1/90 | open |  |  | Donor note | disseminate | Allow | 1/1/90 | open | Grant note |  |  |  |
| service | copyright | copyrighted | 3/15/18 | us | 1/1/00 | open |  |  | Copyright note | publish | Allow | 1/1/00 | open | Grant note |  |  |  |
| service | donor |  |  |  | 1/1/90 | open |  |  | Donor note | disseminate | Allow | 1/1/90 | open | Grant note |  |  |  |
|  |

## Copy transfer to Transfer Source	