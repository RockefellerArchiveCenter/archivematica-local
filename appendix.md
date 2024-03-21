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
| Store DIP                                                                       | Yes    |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |


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
| Store DIP                                                                       | Do not store    |  |
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
| Store DIP                                                                       | none   |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |

### Born Digital 

These should be the default settings for born digital materials ingested from Aurora:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Scan for viruses?                                                               | No     |  |
| Assign UUIDs to directories                                                     | Yes    |  |
| Generate transfer structure report                                              | No     | Since the structure of the transfer is not changed during ingest, this is not necessary |
| Perform file format identification  (Transfer)                                  | Yes    |  |
| Extract packages                                                                | No     |  |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs BulkExtractor; unclear what the benefits are of doing this at ingest |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Perform file format identification  (Ingest)                                    | Yes    |  |
| Normalize                                                                       | Normalize for preservation and access |  |
| Approve normalization                                                           | Yes    |  |
| Choose thumbnail mode                                                           | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     |  |
| Document empty directories                                                      | Yes    |  |
| Reminder: add metadata if desired                                               | Continue |  |
| Transcribe SIP contents                                                         | No     |  |
| Perform file format identification command (Submission documentation & metadata) | Yes |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes   |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Upload DIP                                                                       | Do not upload DIP |  |
| Store DIP                                                                       | Yes   |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |


## FPR Customatizations

The following customizations have been added to the Format Policy Registry (the "Preservation Planning" tab):

### Characterization Rules

*  ffprobe and MediaInfo should be disabled for JPG and TIFF files, as ExifTool is sufficient for characterizing these formats
*  ffprobe and ExifTool should be disabled for moving image files, as MediaInfo is sufficient for characterizing these formats
