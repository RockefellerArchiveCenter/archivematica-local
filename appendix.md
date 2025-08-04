---
layout: docs
title:  "RAC Archivematica | Appendix"
---

## Processing Configuration

### Digitized - Automated

These should be the default settings for digitized materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Scan for viruses?                                                               | No     |  |
| Assign UUIDs to directories                                                     | No     |  |
| Generate transfer structure report                                              | No     |  |
| Perform file format identification (Transfer)                                   | No     | Digitized ingests contain a small set of known file formats |
| Extract packages                                                                | No     | Digitized ingests should not contain packages (e.g., zip files) |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs Bulk Extractor - not necessary for digitized materials, which are already processed |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Perform file format identification (Ingest)                                     | No      |  |
| Normalize                                                                       | Do not normalize | Access derivatives are created in a separate application |
| Approve normalization                                                           | Yes   |  |
| Choose thumbnail mode                                                           | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     | This functionality is not currently used |
| Document empty directories                                                      | No     | Empty directories do not exist in RAC-created transfers |
| Reminder: add metadata if desired                                               | Continue | Digitized ingests include a rights.csv file, so metadata does not need to be added manually |
| Transcribe SIP contents                                                         | No     | This uses Tesseract to OCR TIFs; OCR workflows for digitization happen outside of Archivematica |
| Perform file format identification command (Submission documentation & metadata) | No |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes    |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Upload DIP                                                                      | Do not upload DIP |  |
| Store DIP                                                                       | Reject DIP    | Access copies are created outside of Archivematica |
| Store DIP location                                                              | None |  |


### Digitized AV - Automated

These should be the default settings for digitized audiovisual materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Scan for viruses?                                                               | No     |  |
| Assign UUIDs to directories                                                     | No     |  |
| Generate transfer structure report                                              | No     |  |
| Perform file format identification (Transfer)                                   | No     | Digitized ingests contain a small set of known file formats |
| Extract packages                                                                | No     | Digitized ingests should not contain packages (e.g., zip files) |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs Bulk Extractor - not necessary for digitized materials, which are already processed |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Perform file format identification (Ingest)                                     | No      |  |
| Normalize                                                                       | Do not normalize | Access derivatives are created in a separate application |
| Approve normalization                                                           | Yes   |  |
| Choose thumbnail mode                                                           | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     | This functionality is not currently used |
| Document empty directories                                                      | No     | Empty directories do not exist in RAC-created transfers |
| Reminder: add metadata if desired                                               | Continue | Digitized ingests include a rights.csv file, so metadata does not need to be added manually |
| Transcribe SIP contents                                                         | No     | This uses Tesseract to OCR TIFs; OCR workflows for digitization happen outside of Archivematica |
| Perform file format identification command (Submission documentation & metadata) | No |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes    |  |
| Store AIP location                                                              | Digitized AV AIP Store | Digitized AV should be stored in an S3 bucket |
| Upload DIP                                                                      | Do not upload DIP |  |
| Store DIP                                                                       | Reject DIP    | Access copies are created outside of Archivematica |
| Store DIP location                                                              | None |  |


### Legacy Born Digital - Automated

Legacy born digital materials are those that have been recoverd from digital media items or otherwise accessioned outside of Aurora, and have been fully processed by a processing archivist before ingest into Archivematica. These should be the default settings for legacy born digital materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Scan for viruses?                                                               | No     |  |
| Assign UUIDs to directories                                                     | No     |  |
| Send transfer to quarantine                                                     | No     |  |
| Remove from quarantine after \_\_ days                                          | 28     |  |
| Generate transfer structure report                                              | No     |  |
| Perform file format identification (Transfer)                                   | Yes    |  |
| Extract packages                                                                | No     |  |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     |  |
| Examine contents                                                                | Skip examine contents |  |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Perform file format identification (Ingest)                                     | Yes    |  |
| Normalize                                                                       | Normalize for preservation and access |  |
| Approve normalization                                                           | Yes    |  |
| Choose thumbnail mode                                                           | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     |  |
| Document empty directories                                                      | No     |  |
| Reminder: add metadata if desired                                               | Continue |  |
| Transcribe SIP contents                                                         | No     |  |
| Perform file format identification command (Submission documentation & metadata) | No |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes   |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Upload DIP                                                                      | Do not upload DIP |  |
| Store DIP                                                                       | Reject DIP   | Access copies are created outside of Archivematica |
| Store DIP location                                                              | None |  |

### Born Digital - Automated

This is the processing configuration named "automated" for born digital materials ingested from Aurora:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Scan for viruses?                                                               | No     | Transfers coming through Aurora undergo virus checking|
| Assign UUIDs to directories                                                     | Yes    | Provides more contextual information about folders within a transfer which can assist processing archivists  |
| Generate transfer structure report                                              | No     | Since the structure of the transfer is not changed during ingest, this is not necessary |
| Perform file format identification  (Transfer)                                  | Yes    | Provides information about the file types within the transfer which allows archivists to decide on access and preservation steps |
| Extract packages                                                                | No     | If there are any compressed folders within a transfer, decisions on extraction will be made by the processing archivist |
| Delete packages after extraction                                                | No    | Because there are not any directories being uncompressed within a transfer, there will not be any extracted packages requiring deletion  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs BulkExtractor; unclear what the benefits are of doing this at ingest |
| Create SIP(s)                                                                   | Create single SIP and continue processing | Avoid sending packages to temp storage and creating a backlog for processing |
| Perform file format identification  (Ingest)                                    | No    | No changes have occurred to the transfer packages (such as extraction of packages) so the file format identification would be the same, existing data will be used |
| Normalize                                                                       | Normalize for preservation | Access copies are created and uploaded to access systems with other microservices outside of Archivematica |
| Approve normalization                                                           | Yes    | Normalization rules are set in the Format Policy Registry |
| Choose thumbnail mode                                                           | No     | Thumbnails are not used in any RAC systems |
| Perform policy checks on preservation derivatives                               | No     | This step applies only to AV materials, which are out of scope for this configuration |
| Perform policy checks on access derivatives                                     | No     | This step applies only to AV materials, which are out of scope for this configuration |
| Bind PIDs                                                                       | No     | PIDs in Archivematica are only Handle.Net IDs which are not used by the RAC |
| Document empty directories                                                      | No    | In line with physical material processing guidelines, the RAC does not maintain records of empty folders |
| Reminder: add metadata if desired                                               | Continue | Metadata has been packaged with the content in Aurora |
| Transcribe SIP contents                                                         | No     | The OCR tool in Archivematica does not meet RAC needs |
| Perform file format identification command (Submission documentation & metadata) | No | Creates an unnecessary excess documentation about non-collection materials to be preserved |
| Select compression algorithm                                                    | 7z using bzip2 | Default algothrithm in Archivematica and in line with other RAC processing configurations |
| Select compression level                                                        | 5 - normal compression mode | Normal compression mode meets the RAC's needs for a moderately compressed file |
| Store AIP                                                                       | Yes   | Archivematica AIPs are the RAC's primary archival copy for born-digital materials |
| Store AIP location                                                              | Store AIP in standard Archivematica directory | Storage location defined for maintaining AIPs for born digital content packages |
| Upload DIP                                                                       | Do not upload DIP | Archivematica does not have integrations with the access systems at the RAC  |
| Store DIP                                                                       | Reject DIP   | Access copies are created outside of Archivematica |
| Store DIP location                                                              | None | The RAC does not store Archivematica DIPs |


## FPR Customatizations

The following customizations have been added to the Format Policy Registry (the "Preservation Planning" tab):

### Characterization Rules

*  ffprobe and MediaInfo should be disabled for JPG and TIFF files, as ExifTool is sufficient for characterizing these formats
*  ffprobe and ExifTool should be disabled for moving image files, as MediaInfo is sufficient for characterizing these formats
