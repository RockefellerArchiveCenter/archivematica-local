---
layout: docs
title:  "Administration"
---
## Administration Tab in Dashboard

### Processing Configuration
The processing configuration administration page of the dashboard allows users to configure the job decision points presented by Archivematica during transfer and ingest. This screen provides you with an easy form to configure the default processingMCP.xml that governs these decisions. When you change the options using the web interface the necessary XML will be written behind the scenes.

For the processing configuring for each workflow, please see the appendix.

### Failures
Failed ingests can be viewed and deleted here.

### Locations
The  transfer source locations and AIP storage locations can be viewed in the Administration tab, but are managed in the Storage Service.

The processing storage usage page displays various processing locations with their current usage of available space. Administrators can use the “clear” buttons to delete the contents of these processing locations to make more room on their server.


### DIP Upload (ArchivesSpace)
Before ingesting digital objects destined for ArchivesSpace, ensure that the ArchivesSpace DIP upload settings in the administration tab of the dashboard have been set.

These settings need to be configured before digital objects destined for upload to ArchivesSpace are processed. These should be set once--i.e., they do not need to be re-set for each transfer.

In order to save changes to the ArchivesSpace DIP upload configuration, you must enter the password before clicking save. Note that Archivematica will *not* show you an error if the password is not entered.

The development dashboard should use the ArchivesSpace development IP address, and the production dashboard should use the ArchivesSpace productin IP address.

### PREMIS agent


### REST API

### Users
Users can be also created, modified and deleted from the Administration tab. Only users who are administrators can create and edit user accounts.

* _Add new:_ add a new user to the Archivematica dashboard.
* _Edit:_ change a user's username or password.
* _Delete:_ revoke a user's access.

### Handle server config

### Language

### Version

## Storage Service

The Archivematica Storage Service allows the configuration of storage spaces associated with multiple Archivematica pipelines. It allows a storage administrator to configure what storage is available to each Archivematica installation, both locally and remote. The Storage Service is a separate application from the Dashboard; stored AIPs can be viewed in the `Archival storage` tab in the Archivematica dashboard.

The Storage Service is the mechanism by which Archivematica is able to store packages and manage file locations, such as transfer source locations. Responsibilies for the Storage Service should be assigned to one Administrative user who will be responsible for managing locations and AIP deletion requests.

The storage service is organized into four different entities: spaces, locations, pipelines, packages.

*  **Spaces:** A space models a specific storage device. That device might be a locally- accessible disk, a network share, or a remote system accessible via a protocol like FEDORA, SWIFT, DuraCloud, or LOCKSS. The space provides the Storage Service with configuration to read and/or write data stored within itself.
*  **Locations:** A location is a subdivision of a space. Each location is assigned a specific purpose, such as AIP storage, DIP storage, transfer source or transfer backlog, in order to provide an organized way to structure content within a space.
*  **Pipelines:** A pipeline refers to a single installation of an Archivematica dashboard. The Storage Service can be used to configure spaces and locations across multiple Archivematica pipelines.
*  **Packages:** The Storage Service is oriented to storing packages. A “package” is a bundle of one or more files transferred from an external service; for example, a package may be an AIP, a backlogged transfer, or a DIP. Each package is stored in a location.


### Spaces
A storage Space contains all the information necessary to connect to the physical storage. It is where protocol-specific information, like an NFS export path and hostname, or the username of a system accessible only via SSH, is stored. All locations must be contained in a space.

A space is usually the immediate parent of the Location folders. For example, if you had transfer source locations at /home/artefactual/archivematica- sampledata-2013-10-10-09-17-20 and /home/artefactual/maildir_transfers, the Space’s path would be /home/artefactual/

Currently supported protocols are local filesystem, NFS, pipeline local filesystem, LOCKSS, DuraCloud, Arkivum, Fedora and Swift. The RAC currently uses, or may in the future use, local filesystem, NFS, pipeline local filesystem, LOCKSS, and Fedora.

*  Local Filesystem spaces handle storage that is available locally on the machine running the storage service. Typically this is the hard drive, SSD or raid array attached to the machine, but it could also encompass remote storage that has already been mounted. For remote storage that has been locally mounted, we recommend using a more specific Space if one is available.
*  NFS spaces are for NFS exports mounted on the Storage Service server, and the Archivematica pipeline.
*  Pipeline Local Filesystems refer to the storage that is local to the Archivematica pipeline, but remote to the storage service. For this Space to work properly, passwordless SSH must be set up between the Storage Service host and the Archivematica host. For example, the storage service is hosted on storage_service_host and Archivematica is running on archivematica1 . The transfer sources for Archivematica are stored locally on archivematica1, but the storage service needs access to them. The Space for that transfer source would be a Pipeline Local Filesystem.
*  Archivematica can store AIPs in a LOCKSS network via LOCKSS-O-Matic, which uses SWORD to communicate between the Storage Service and a Private LOCKSS Network (PLN). When creating a Location for a LOCKSS space, the Purpose of the Location must be AIP Storage.
*  Fedora via SWORD2 is currently supported in the Storage Service as an Access Protocol to facilitate use of the Archidora plugin, which allows ingest of material from Islandora to Archivematica. This workflow is in beta testing as of Storage Service 0.9/Archivematica 1.5/Islandora 7.x-1.6.


### Locations

A storage Location is contained within a Space, and knows its purpose in the Archivematica system. Each Location is associated with at least one pipeline; with the exception of Backlog and Currently Processing locations, for which there must be exactly one per pipeline, a pipeline can have multiple instances of any location, and a location can be associated with any number of pipelines. For Spaces of the type “Local Filesystem,” Locations are basically directories (or more accurately, paths to directories). You can create Locations for Transfer Source, Currently Processing, or AIP and DIP Storage. Currently, a Location can have one of eight purposes:

*  Transfer Source: Transfer source locations display in Archivematica’s Transfer tab, and any folder in a transfer source can be selected to become a Transfer. The default value is ‘/home’ in a Local Filesystem. This is required to start transfers.
*  Transfer Backlog: Transfer backlog stores transfers until such a time that the user continues processing them. The default value is ‘/var/archivematica/sharedDirectory/www/AIPsStore/transferBacklog’ in a Local Filesystem. This is required to store and retrieve transfers in backlog.
*  AIP Storage: AIP storage locations are where the completed AIPs are put for long-term storage. The default value is ‘/var/archivematica/sharedDirectory/www/AIPsStore’ in a Local Filesystem. This is required to store and retrieve AIPs.
*  DIP Storage: Likewise, DIP storage is used for storing DIPs until such a time that they can be uploaded to an access system. The default value is ‘/var/archivematica/sharedDirectory/www/DIPsStore’ in a Local Filesystem. This is required to store and retrieve DIPs. This is not required to upload DIPs to access systems.
*  Currently Processing: During processing, Archivematica uses the currently processing location associated with that pipeline. Exactly one currently processing location should be associated with a given pipeline. The default value is ‘/var/archivematica/sharedDirectory’ in a Local Filesystem. This is required for Archivematica to run.
*  Storage Service Internal Processing: Likewise, there should only be exactly one Storage Service Internal Processing location for each Storage Service installation. The default value is ‘/var/archivematica/storage_service’ in a Local Filesystem. This is required for the Storage Service to run, and must be locally available to the storage service. It should not be associated with any pipelines.
*  AIP Recovery: AIP Recovery is where the AIP recovery feature looks for an AIP to recover. No more than one AIP recovery locatio should be associated with a given pipeline. The default value is ‘/var/archivematica/storage_service/recover’ in a Local Filesystem. This is only required if AIP recovery is used.
*  FEDORA Deposit: FEDORA Deposit is used with the Archidora plugin to ingest material from Islandora. This is only available to the FEDORA Space, and is only required for that space.

Replicator locations can be configured to replicate the AIPs in one or more AIP storage locations.

### Administration
The Administration section manages the users and settings for the Storage Service.

*  USERS: Only registered users can long into the storage service, and the Users page is where users can be created or modified. The storage service has two types of users: administrative users, and regular users. The only distinction between the two types is for email notifications; administrators will be notified by email when special events occur, while regular users will not.
*  SETTINGS: Settings control the behavior of the Storage Service. Default Locations are the created or associated with pipelines when they are created.
*  VERSION: The version page will display the current version and specific git commit of your installation of the Storage Service.
*  SERVICE CALLBACKS: Callbacks allow REST calls to be made by the Archivematica Storage Service after performing certain types of actions. This allows external services to be notified when internal actions have taken place.