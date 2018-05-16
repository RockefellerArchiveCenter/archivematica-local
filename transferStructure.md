---
layout: docs
title:  "Transfer Structure"
---

## Structuring the transfer 

While Archivematica will restructure a directory for basic transfers, some transfer types require a directory structure that is compliant with Archivematica's SIP directory structure. A structured directory is required for the following types of transfers:

*  transfers with multiple versions of digitized files
*  transfer with metadata, such as an archivesspaceids.csv or rights.csv
*  transfers with manually normalized files
*  transfers with submission documention

As these are the vast majority of our use cases, all transfers ingested into Archivematica should be in a structured directory. A structured directory includes the following subdirectories:

*  **objects**: The objects directory contains the digital objects that are to be preserved. You can create subdirectories within objects if desired.
*  **metadata**: The metadata directory contains the checksum, the METS file, and a submissionDocumentation subfolder, which can be used for transfer forms, donation agreements or any other documents that relate to the acquisition of the records.
*  **logs**: The logs directory will eventually contain logs generated when processing the transfer in Archivematica.

## Digitized

Master files are in directory "Master," master edited files are in directory "Master Edited," and serviced edited files are in directory "Service Edited." The output should look like either of the following (depending on access format):


### Access format: concatenated PDF

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

### Access format: JPGs

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

## Legacy Born Digital

### With Manually Normalized Files

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

### Without Manually Normalized Files

```
 /top-level                                                               
   /objects                                                                 
     digital-object1.pdf                                                      
     digital-object2.pdf                                                      
     digital-object3.docx                                                     
   /metadata                                                                
     archivesspaceids.csv\                                                    
     /submissionDocumentation                                                 
       FTKExportSummary1.txt                                                                                                                        
   /logs                                                                    
```