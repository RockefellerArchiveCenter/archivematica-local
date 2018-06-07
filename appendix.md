---
layout: docs
title:  "Appendix"
---

## Processing Configuration

### Digitized

These should be the default settings for digitized materials:

|  Step                                                                            |  Action |
|  ------------------------------------------------------------------------------- | ------- |
|  Assign UUIDs to directories                                                     | No |
|  Send transfer to quarantine                                                     | No |
|  Remove from quarantine after \_\_ days                                          | 28 |
|  Generate transfer structure report                                              | No |
|  Select file format identification command (Transfer)                            | Skip file identification |
|  Extract packages                                                                | No |
|  Delete packages after extraction                                                | Yes |
| Perform policy checks on originals                                               | No |
|  Examine contents                                                                | Skip examine contents |
|  Create SIP(s)                                                                   | Create single SIP and continue processing |
|  Select file format identification command (Ingest)                              | Use existing data |
|  Normalize                                                                       | Do not normalize |
|  Approve normalization                                                           | None |
| Perform policy checks on preservation derivatives                                | No |
| Perform policy checks on access derivatives                                      | No |
| Bind PIDs                                                                        | No |
| Document empty directories                                                       | No |
|  Reminder: add metadata if desired                                               | Continue |
|  Transcribe files (OCR)                                                          | No |
|  Select file format identification command (Submission documentation & metadata) | File extension |
|  Select compression algorithm                                                    | 7z using bzip2 |
|  Select compression level                                                        | 5 - normal compression mode |
|  Store AIP                                                                       | none |
|  Store AIP location                                                              | Store AIP in standard Archivematica directory |
|  Store DIP                                                                       | none |
|  Store DIP location                                                              | Store DIP in standard Archivematica directory |

### Born Digital

These should be the default settings for born digital materials:

|  Step                                                                            |  Action |
|  ------------------------------------------------------------------------------- | ------- |
|  Assign UUIDs to directories                                                     | No |
|  Send transfer to quarantine                                                     | No |
|  Remove from quarantine after \_\_ days                                          | 28 |
|  Generate transfer structure report                                              | No |
|  Select file format identification command (Transfer)                            | File extension |
|  Extract packages                                                                | No |
|  Delete packages after extraction                                                | Yes |
| Perform policy checks on originals                                               | No |
|  Examine contents                                                                | Skip examine contents |
|  Create SIP(s)                                                                   | Create single SIP and continue processing |
|  Select file format identification command (Ingest)                              | Identify using Fido |
|  Normalize                                                                       | Normalize for preservation and access |
|  Approve normalization                                                           | Yes |
| Perform policy checks on preservation derivatives                                | No |
| Perform policy checks on access derivatives                                      | No |
| Bind PIDs                                                                        | No |
| Document empty directories                                                       | No |
|  Reminder: add metadata if desired                                               | Continue |
|  Transcribe files (OCR)                                                          | No |
|  Select file format identification command (Submission documentation & metadata) | File extension |
|  Select compression algorithm                                                    | 7z using bzip2 |
|  Select compression level                                                        | 5 - normal compression mode |
|  Store AIP                                                                       | none |
|  Store AIP location                                                              | Store AIP in standard Archivematica directory |
|  Store DIP                                                                       | none |
|  Store DIP location                                                              | Store DIP in standard Archivematica directory |

## PREMIS Mapping

### Data mapping

#### Basic information

*  **Title:** Derive from original filename of digital object.
*  **Identifier:** Populate with Archivematica DIP URI without digital object filename.
*  **Publish:** Set as TRUE or FALSE based on PREMIS statement (see Publish: Base on PREMIS below).
*  **Type:** Populate with value from Object Type field in Archivematica administration settings. If no data entered in this field, leave empty.
*  **Language:** Derive from parent component in ArchivesSpace.
*  **Restrictions?: Set as TRUE or FALSE based on PREMIS statement (see Restrictions:** Base on PREMIS below).

#### File Version

*  **File URI: Populate with URL prefix from URI Prefix field in  Archivematica administration settings, plus file UUID and filename, for example: http:**//storage.rockarch.org/[UUID]-filename.
*  **Use Statement:** Populate with value from Use Statement field in Archivematica administration settings.
*  **XLink Attribute Actuate: Derive from PREMIS statement (see Restrictions:** Base on PREMIS below). If no PREMIS statements are present, base on value from XLink Attribute Actuate field in Archivematica administration settings.
*  **XLink Show Attribute: Derive from PREMIS statement (see Restrictions:** Base on PREMIS below). If no PREMIS statements are present, base on value from XLink Show Attribute field in Archivematica administration settings.
*  **File Format Name:** Populate with DIP digital object file format name as identified by Archivematica.
*  **File Format Version:** Populate with DIP digital object file format version as identified by Archivematica.
*  **File Size:** Populate with DIP digital object file size measured in bytes, as identified by Archivematica.

#### Notes

*  **Conditions Governing Access note: Derive from PREMIS <rightsGrantedNote> (see Restrictions:** Base on PREMIS below). If there is no content in <rightsGrantedNote>, populate with value from Conditions Governing Access field in Archivematica administration settings. If no data is entered in this field, do not add note.
*  **Conditions Governing Use note: Derive from PREMIS <rightsGrantedNote> (see Restrictions:** Base on PREMIS below). If there is no content in <rightsGrantedNote>, populate with value from Conditions Governing Use field in Archivematica administration settings. If no data is entered in this field, do not add note.
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

*  If PREMIS <act> = Disseminate and PREMIS <restriction> = Allow, Restrictions? = FALSE
*  If PREMIS <act> = Disseminate and PREMIS <restriction> = Conditional, Restrictions? = TRUE
*  If PREMIS <act> = Disseminate and PREMIS <restriction> = Disallow, Restrictions? = TRUE
*  If PREMIS <act> = Disseminate, populate Conditions Governing Access note with contents of PREMIS rightsGrantedNote
*  When Restrictions?=TRUE, both XLink Attribute Actuate and XLink Attribute Show will be set to “none.”

#### Publish

*  If PREMIS <act> = Publish, populate ConditionsGoverningUse with contents of PREMIS rightsGrantedNote

### Publish: Base on PREMIS

*  If PREMIS <act> = Disseminate and PREMIS <restriction> = Allow, Publish = TRUE
*  If PREMIS <act> = Disseminate and PREMIS <restriction> = Conditional, Publish = FALSE
*  If PREMIS <act> = Disseminate and PREMIS <restriction> = Disallow, Publish = FALSE
	
## Troubleshooting

