---
layout: docs
title:  "RAC Archivematica | Appendix"
---

## Processing Configuration

### Digitized

These should be the default settings for digitized materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Assign UUIDs to directories                                                     | No     |  |
| Send transfer to quarantine                                                     | No     |  |
| Remove from quarantine after \_\_ days                                          | 28     |  |
| Generate transfer structure report                                              | No     |  |
| Perform file format identification (Transfer)                                   | No     | Digitized ingests contain a small set of known file formats |
| Extract packages                                                                | No     | Digitized ingests should not contain packages (e.g., zip files) |
| Delete packages after extraction                                                | Yes    |  |
| Perform policy checks on originals                                              | No     | Policy checks refers to MediaConch, which is only used for A/V |
| Examine contents                                                                | Skip examine contents | Runs Bulk Extractor - not necessary for digitized materials, which are already processed |
| Create SIP(s)                                                                   | Create single SIP and continue processing |  |
| Perform file format identification (Ingest)                                     | No      |  |
| Normalize                                                                       | Do not normalize | Digitized ingests contain preservation masters, as well as an `access` directory that will generate a DIP |
| Approve normalization                                                           | None   |  |
| Generate thumbnails                               | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     | This functionality is not currently used |
| Document empty directories                                                      | No     | Empty directories do not exist in RAC-created transfers |
| Reminder: add metadata if desired                                               | Continue | Digitized ingests include a rights.csv file, so metadata does not need to be added manually |
| Transcribe files (OCR)                                                          | No     | This uses Tesseract to OCR TIFs; RAC digitized transfers include access PDFs that have already been OCR'd |
| Perform file format identification command (Submission documentation & metadata) | No |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes    |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Upload DIP                                                                       | Upload DIP to ArchivesSpace |  |
| Store DIP                                                                       | Yes    |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |

### Legacy Born Digital

Legacy born digital materials are those that have been recoverd from digital media items or otherwise accessioned outside of Aurora, and have been fully processed by a processing archivist before ingest into Archivematica. These should be the default settings for legacy born digital materials:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
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
| Generate thumbnails                               | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     |  |
| Document empty directories                                                      | No     |  |
| Reminder: add metadata if desired                                               | Continue |  |
| Transcribe files (OCR)                                                          | No     |  |
| Perform file format identification command (Submission documentation & metadata) | No |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | none   |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Upload DIP                                                                       | Upload DIP to ArchivesSpace |  |
| Store DIP                                                                       | none   |  |
| Store DIP location                                                              | Store DIP in standard Archivematica directory |  |

### Born Digital

These should be the default settings for born digital materials ingested from Aurora:

| Step                                                                            | Action | Rationale |
| ------------------------------------------------------------------------------- | ------ | --------- |
| Assign UUIDs to directories                                                     | Yes    |  |
| Send transfer to quarantine                                                     | No     |  |
| Remove from quarantine after \_\_ days                                          | 28     |  |
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
| Generate thumbnails                               | No     |  |
| Perform policy checks on preservation derivatives                               | No     |  |
| Perform policy checks on access derivatives                                     | No     |  |
| Bind PIDs                                                                       | No     |  |
| Document empty directories                                                      | Yes    |  |
| Reminder: add metadata if desired                                               | Continue |  |
| Transcribe files (OCR)                                                          | No     |  |
| Perform file format identification command (Submission documentation & metadata) | Yes |  |
| Select compression algorithm                                                    | 7z using bzip2 |  |
| Select compression level                                                        | 5 - normal compression mode |  |
| Store AIP                                                                       | Yes   |  |
| Store AIP location                                                              | Store AIP in standard Archivematica directory |  |
| Upload DIP                                                                       | Do not upload DIP |  |
| Store DIP                                                                       | Yes   |  |
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

## FPR Customatizations

The following customizations have been added to the Format Policy Registry (the "Preservation Planning" tab):

### Characterization Rules

*  ffprobe and MediaInfo should be disabled for JPG and TIFF files, as ExifTool is sufficient for characterizing these formats

## Upgrading to a new release of Archivematica

### 1. Review Release Notes (Archivematica Product Owner)

Review release notes made available on Archivematica wiki, noting any changes that may impact RAC workflows or the upgrade process. If skipping versions (e.g., from 1.7 to 1.9), review release notes for intermediate versions.

### 2. Plan Upgrade (Archivematica Product Owner)

Coordinate with Artefactual, RAC Information Systems Manager, and other key [RAC staff](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) to plan upgrade at least 3 weeks in advance. Production and development upgrade should be planned at the same time, with production scheduled for 2 weeks after development. The upgrade schedule will likely look like:

* Week 1: Set up development VMs, upgrade development
* Week 2: Upgrade integrated applications, test development
* Week 3: Set up production VMs, upgrade production
* Week 4: Upgrade integrated applications, test production

### 3. Set up Development VMs (Information Systems Manager) (optional)

This is only necessary if the Archivematica upgrade involves a move to new VMs. This step includes:

* Setting up dev VMs in accordance with [current specs](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/)
* Setting up ssh access for [select RAC staff](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) for VMs
* Setting up all accounts and access for Artefactual
* Configuring [DNS](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/

When this is complete, convey information about IPs and logins to the Archivematica Product Owner so that she can update the Archivematica Info Sheet, inform key staff, and let Artefactual know our development environment is ready to be upgraded.

### 4. Upgrade (Artefactual)

Archivematica Product Owner alerts key staff to window where Archivematica development environment will be down. Artefactual upgrades both pipelines and the storage service in our dev environment.

### 5. Update Integrated Applications in Development Environment (Archivematica Product Owner)

Review whether user accounts, API Keys, and Pipeline and Location UUIDs have changed, and work with key staff to update configs in other applications as necessary. Connected applications may include Fornax and Gemini.

### 6. Test on Development (Archivematica Product Owner)

Along with key staff, test the following:

* All expected [user accounts](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) are present
* Transfers can be sent to and stored in all locations on both pipelines
* All integrations work as expected

Errors as they occur will be communicated to the Archivematica Product Owner, who will work with Artefactual to resolve them. When testing is complete, the Archivematica Product Owner will alert Artefactual and the Information Systems Manager.

### 7. Set up Production VMs (Information Systems Manager) (optional)

This is only necessary if the Archivematica upgrade involves moving to new VMs. This step includes:

* Setting up dev VMs in accordance with [current specs](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/)
* Setting up ssh access for [select RAC staff](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) for VMs
* Setting up all accounts and access for Artefactual
* Configuring [DNS](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/

### 8. Upgrade (Artefactual)

Archivematica Product Owner alerts key staff to window where Archivematica production environment will be down. Artefactual upgrades both pipelines and the storage service in our production environment.

### 9. Update Integrated Applications (Archivematica Product Owner)

Review whether user accounts, API Keys, and Pipeline and Location UUIds have changed, and work with key staff to update configs in other applications as necessary. Connected applications may include Fornax and Gemini.

### 10. Test on Production (Archivematica Product Owner)

Along with key staff, test the following:

* All expected [user accounts](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) are present
* Transfers can be sent to and stored in all locations on both pipelines
* All integrations work as expected

Errors will be reported to the Archivematica Product Owner, who will work with Artefactual to resolve them. When testing is complete, the Archivematica Product Owner will alert Artefactual and key staff.
