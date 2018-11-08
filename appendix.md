---
layout: docs
title:  "RAC Archivematica | Appendix"
---

## Processing Configuration

### Digitized

These should be the default settings for digitized materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ |  |
| Assign UUIDs to directories                                                     | No     |  |
| Send transfer to quarantine                                                     | No     |  |
| Remove from quarantine after \_\_ days                                          | 28     |  |
| Generate transfer structure report                                              | No     |  |
| Select file format identification command (Transfer)                            | File extension | Digitized ingests contain a small set of known file formats |
| Extract packages                                                                | No     | Digitized ingests should not contain packages (e.g., zip files) |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs Bulk Extractor - not necessary for digitized materials, which are already processed |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Select file format identification command (Ingest)                              | Use existing data |  |
| Normalize                                                                       | Do not normalize | Digitized ingests contain preservation masters, as well as an `access` directory that will generate a DIP |
| Approve normalization                                                           | None   |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     | This functionality is not currently used |
| Document empty directories                                                      | No     | Empty directories do not exist in RAC-created transfers |
| Reminder: add metadata if desired                                               | Continue | Digitized ingests include a rights.csv file, so metadata does not need to be added manually |
| Transcribe files (OCR)                                                          | No     | This uses Tesseract to OCR TIFs; RAC digitized transfers include access PDFs that have already been OCR'd |
| Select file format identification command (Submission documentation & metadata) | File extension |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes    |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Store DIP                                                                       | Yes    |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |

### Legacy Born Digital

Legacy born digital materials are those that have been recoverd from digital media items or otherwise accessioned outside of Aurora, and have been fully processed by a processing archivist before ingest into Archivematica. These should be the default settings for legacy born digital materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ |  |
| Assign UUIDs to directories                                                     | No     |  |
| Send transfer to quarantine                                                     | No     |  |
| Remove from quarantine after \_\_ days                                          | 28     |  |
| Generate transfer structure report                                              | No     |  |
| Select file format identification command (Transfer)                            | Identify using Siegfried |  |
| Extract packages                                                                | No     |  |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     |  |
| Examine contents                                                                | Skip examine contents |  |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Select file format identification command (Ingest)                              | Identify using Fido |  |
| Normalize                                                                       | Normalize for preservation and access |  |
| Approve normalization                                                           | Yes    |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     |  |
| Document empty directories                                                      | No     |  |
| Reminder: add metadata if desired                                               | Continue |  |
| Transcribe files (OCR)                                                          | No     |  |
| Select file format identification command (Submission documentation & metadata) | File extension |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | none   |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Store DIP                                                                       | none   |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |

### Born Digital

These should be the default settings for born digital materials ingested from Aurora:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ |  |
| Assign UUIDs to directories                                                     | No     | Since directory structure conforms to RAC spec, this is not necessary |
| Send transfer to quarantine                                                     | No     |  |
| Remove from quarantine after \_\_ days                                          | 28     |  |
| Generate transfer structure report                                              | No     | Since the structure of the transfer is not changed during ingest, this is not necessary |
| Select file format identification command (Transfer)                            | Identify using Siegfried |  |
| Extract packages                                                                | ???     |  |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs BulkExtractor; unclear what the benefits are of doing this at ingest |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Select file format identification command (Ingest)                              | Identify using Fido |  |
| Normalize                                                                       | Normalize for preservation | DIP generation not used in this workflow |
| Approve normalization                                                           | Yes    |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     |  |
| Document empty directories                                                      | No     |  |
| Reminder: add metadata if desired                                               | Continue |  |
| Transcribe files (OCR)                                                          | No     |  |
| Select file format identification command (Submission documentation & metadata) | File extension |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | none   |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Store DIP                                                                       | none   |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |

## PREMIS Mapping

### Data mapping

#### Basic information

*  **Title:** Derive from original filename of digital object.
*  **Identifier:** Populate with Archivematica DIP URI without digital object filename.
*  **Publish:** Set as TRUE or FALSE based on PREMIS statement (see Publish: Base on PREMIS below) or administration settings.
*  **Type:** Populate with value from Object Type field in Archivematica administration settings. If no data entered in this field, leave empty.
*  **Language:** Derive from parent component in ArchivesSpace.
*  **Restrictions?:** Set as TRUE or FALSE based on PREMIS statement (see Restrictions: Base on PREMIS below) or administration settings.

#### File Version

*  **File URI:** Populate with URL prefix from URI Prefix field in  Archivematica administration settings, plus file UUID and filename, for example: http://storage.rockarch.org/[UUID]-filename.
*  **Use Statement:** Populate with value from Use Statement field in Archivematica administration settings.
*  **XLink Attribute Actuate:** Base on value from XLink Attribute Actuate field in Archivematica administration settings.
*  **XLink Show Attribute:** Base on value from XLink Show Attribute field in Archivematica administration settings.
*  **File Format Name:** Populate with DIP digital object file format name as identified by Archivematica.
*  **File Format Version:** Populate with DIP digital object file format version as identified by Archivematica.
*  **File Size:** Populate with DIP digital object file size measured in bytes, as identified by Archivematica.

#### Notes

*  **Conditions Governing Access note:** Derive from PREMIS _rightsGrantedNote_. If there is no content in _rightsGrantedNote_, populate with value from Conditions Governing Access field in Archivematica administration settings. If no data is entered in this field, do not add note.
*  **Conditions Governing Use note:** Derive from PREMIS _rightsGrantedNote_. If there is no content in _rightsGrantedNote_, populate with value from Conditions Governing Use field in Archivematica administration settings. If no data is entered in this field, do not add note.
*  **Existence and Location of Originals note:** automatically populate with Archivematica AIP UUID
*  If specified in administration settings, Any other notes attached to the parent component in ArchivesSpace should also be attached to the digital object record.

#### Agents

*  Any agents linked to the parent component in ArchivesSpace should be linked to the digital object record, if specified in administration settings.
*  Agent records for agents recorded in Archivematica should be created and linked to the digital object record, if specified in administration settings.

#### Subjects
*  Any subjects linked to the parent component in ArchivesSpace should be linked to the digital object record, if specified in administration settings.

#### Record Link
*  Create link to parent component in ArchivesSpace

### Restrictions: Base on PREMIS

#### Disseminate

*  If PREMIS _act_ = Disseminate and PREMIS _restriction_ = Allow, Restrictions? = FALSE
*  If PREMIS _act_ = Disseminate and PREMIS _restriction_ = Conditional, Restrictions? = TRUE
*  If PREMIS _act_ = Disseminate and PREMIS _restriction_ = Disallow, Restrictions? = TRUE
*  If PREMIS _act_ = Disseminate, populate Conditions Governing Access note with contents of PREMIS _rightsGrantedNote_
*  When Restrictions?=TRUE, both XLink Attribute Actuate and XLink Attribute Show will be set to “none.”

#### Publish

*  If PREMIS _act_ = Publish, populate _ConditionsGoverningUse_ with contents of PREMIS rightsGrantedNote

### Publish: Base on PREMIS

*  If PREMIS _act_ = Disseminate and PREMIS _restriction_ = Allow, Publish = TRUE
*  If PREMIS _act_ = Disseminate and PREMIS _restriction_ = Conditional, Publish = FALSE
*  If PREMIS _act_ = Disseminate and PREMIS _restriction_ = Disallow, Publish = FALSE
	