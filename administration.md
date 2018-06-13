---
layout: docs
title:  "RAC Archivematica | Administration"
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
The PREMIS agent information is used in the METS files created by Archivematica to identify the agency performing the digital preservation events.

### REST API

### Users
Users can be also created, modified and deleted from the Administration tab. Only users who are administrators can create and edit user accounts.

* _Add new:_ add a new user to the Archivematica dashboard.
* _Edit:_ change a user's username or password.
* _Delete:_ revoke a user's access.

### Handle server config
The RAC does not use this feature.


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

*  **Transfer Source:** Transfer source locations display in Archivematica’s Transfer tab, and any folder in a transfer source can be selected to become a Transfer. The default value is ‘/home’ in a Local Filesystem. This is required to start transfers.
*  **Transfer Backlog:** Transfer backlog stores transfers until such a time that the user continues processing them. The default value is ‘/var/archivematica/sharedDirectory/www/AIPsStore/transferBacklog’ in a Local Filesystem. This is required to store and retrieve transfers in backlog.
*  **AIP Storage:** AIP storage locations are where the completed AIPs are put for long-term storage. The default value is ‘/var/archivematica/sharedDirectory/www/AIPsStore’ in a Local Filesystem. This is required to store and retrieve AIPs.
*  **DIP Storage:** Likewise, DIP storage is used for storing DIPs until such a time that they can be uploaded to an access system. The default value is ‘/var/archivematica/sharedDirectory/www/DIPsStore’ in a Local Filesystem. This is required to store and retrieve DIPs. This is not required to upload DIPs to access systems.
*  **Currently Processing:** During processing, Archivematica uses the currently processing location associated with that pipeline. Exactly one currently processing location should be associated with a given pipeline. The default value is ‘/var/archivematica/sharedDirectory’ in a Local Filesystem. This is required for Archivematica to run.
*  **Storage Service Internal Processing:** Likewise, there should only be exactly one Storage Service Internal Processing location for each Storage Service installation. The default value is ‘/var/archivematica/storage_service’ in a Local Filesystem. This is required for the Storage Service to run, and must be locally available to the storage service. It should not be associated with any pipelines.
*  **AIP Recovery:** AIP Recovery is where the AIP recovery feature looks for an AIP to recover. No more than one AIP recovery locatio should be associated with a given pipeline. The default value is ‘/var/archivematica/storage_service/recover’ in a Local Filesystem. This is only required if AIP recovery is used.
*  **FEDORA Deposit:** FEDORA Deposit is used with the Archidora plugin to ingest material from Islandora. This is only available to the FEDORA Space, and is only required for that space.

Replicator locations can be configured to replicate the AIPs in one or more AIP storage locations.

### Administration
The Administration section manages the users and settings for the Storage Service.

*  **USERS:** Only registered users can long into the storage service, and the Users page is where users can be created or modified. The storage service has two types of users: administrative users, and regular users. The only distinction between the two types is for email notifications; administrators will be notified by email when special events occur, while regular users will not.
*  **SETTINGS:** Settings control the behavior of the Storage Service. Default Locations are the created or associated with pipelines when they are created.
*  **VERSION:** The version page will display the current version and specific git commit of your installation of the Storage Service.
*  **SERVICE CALLBACKS:** Callbacks allow REST calls to be made by the Archivematica Storage Service after performing certain types of actions. This allows external services to be notified when internal actions have taken place.

## Automation Tools

`transfers/transfer.py` is used to prepare transfers, move them into the pipelines processing location, and take actions when user input is required.
Only one transfer is sent to the pipeline at a time, the scripts wait until the current transfer is resolved (failed, rejected or stored as an AIP) before automatically starting the next available transfer.

### Configuration
Suggested deployment is to use cron to run a shell script that runs the automate transfer tool. Example shell script (for example in `/etc/archivematica/automation-tools/transfer-script.sh`):

```
#!/bin/bash
cd /usr/lib/archivematica/automation-tools/
/usr/share/python/automation-tools/bin/python -m transfers.transfer --user <user> --api-key <apikey> --ss-user <user> --ss-api-key <apikey> --transfer-source <transfer_source_uuid> --config-file <config_file>
```

(Note that the script calls the transfers script as a module using python's `-m` flag, this is required due to the use of relative imports in the code)

The `transfers.py` script can be modified to adjust how automated transfers work.  The full set of parameters that can be changed are:

* `-u USERNAME, --user USERNAME` [REQUIRED]: Username of the Archivematica dashboard user to authenticate as.
* `-k KEY, --api-key KEY` [REQUIRED]: API key of the Archivematica dashboard user.
* `--ss-user USERNAME` [REQUIRED]: Username of the Storage Service user to authenticate as. Storage Service 0.8 and up requires this; earlier versions will ignore any value provided.
* `--ss-api-key KEY` [REQUIRED]: API key of the Storage Service user. Storage Service 0.8 and up requires this; earlier versions will ignore any value provided.
* `-t UUID, --transfer-source UUID`: [REQUIRED] Transfer Source Location UUID to fetch transfers from. Can be found under "Locations" in Storage Service.
* `--transfer-path PATH`: Relative path within the Transfer Source. Default: ""
* `--depth DEPTH, -d DEPTH`: Depth to create the transfers from relative to the transfer source location and path. Default of 1 creates transfers from the children of transfer-path.
* `--am-url URL, -a URL`:Archivematica URL. Default: http://127.0.0.1
* `--ss-url URL, -s URL`: Storage Service URL. Default: http://127.0.0.1:8000
* `--transfer-type TYPE`: Type of transfer to start. One of: 'standard' (default), 'unzipped bag', 'zipped bag', 'dspace'.
* `--files`: If set, start transfers from files as well as folders.
* `--hide`: If set, hides the Transfer and SIP once completed.
* `-c FILE, --config-file FILE`: config file containing file paths for log/database/PID files. Default: log/database/PID files stored in the same directory as the script (not recommended for production)
* `-v, --verbose`: Increase the debugging output. Can be specified multiple times, e.g. `-vv`
* `-q, --quiet`: Decrease the debugging output. Can be specified multiple times, e.g. `-qq`
* `--log-level`: Set the level for debugging output. One of: 'ERROR', 'WARNING', 'INFO', 'DEBUG'. This will override `-q` and `-v`

The `--config-file` specified can also be used to define a list of file extensions that script files should have for execution. By default there is no limitation, but it may be useful to specify this, for example `scriptextensions = .py:.sh`. Multiple extensions may be specified, using '`:`' as a separator.

#### Running the Script
The script can be run from a shell window like:

```
user@host:/etc/archivematica/automation-tools$ sudo -u archivematica ./transfer-script.sh
```

It is suggested to run the script through a crontab entry for user archivematica (to avoid the need to repeatedly invoke it manually):

```
*/5 * * * * /etc/archivematica/automation-tools/transfer-script.sh
```

When running, automated transfers stores its working state in a sqlite database.  It contains a record of all the transfers that have been processed.  In a testing environment, deleting this file will cause the tools to re-process any and all folders found in the Transfer Source Location.

#### Getting Correct UUIDs and Setting Processing Rules

The easiest way to configure the tasks that automation-tools will run is by using the dashboard:

1. Go to Administration > Processing Configuration and choose the options you wish to use.

2. Save the configuration on the form.

3. Copy the processing configuration file from `/var/archivematica/sharedDirectory/sharedMicroServiceTasksConfigs/processingMCPConfigs/defaultProcessingMCP.xml` on the Archivematica host machine to the `transfers/` directory of your automation-tools installation location.

The automation-tools command-line also relies on installation-specific UUIDs. To obtain the transfer source UUID for script invocation, visit the 'Transfer Source' tab in the Archivematica Storage Space web dashboard. If a row is marked as a transfer souce its UUID value will be valid as a transfer source argument.

#### Getting API keys

To get the Archivematica API key, log in to Archivematica as the user you wish to authenticate as.
From the dashboard, click your username in the top right corner, then select 'Your profile'.
The API key will be displayed at the bottom of the page.

To get the Storage Service API key, log in to the Storage Service as the user you wish to authenticate as.
From the dashboard, go to Administration > Users and select 'Edit' for the user you want the key for.
The API key will be displayed at the bottom of the page.

### Hooks

During processing, automate transfers will run scripts from several places to customize behaviour. These scripts can be in any language. If they are written in Python, we recommend making them source compatible with python 2 or 3.

There are three places hooks can be used to change the automate tools behaviour.

* `transfers/get-accession-number` (script)
* `transfers/pre-transfer` (directory)
* `transfers/user-input` (directory)

Any new scripts added to these directories will automatically be run alongside the existing scripts.

There are also several scripts provided for common use cases and examples of processing that can be done.
These are found in the `examples` directory sorted by their usecase and can be copied or symlinked to the appropriate directory for automation-tools to run them.
If you write a script that might be useful for others, please make a pull request!

#### get-accession-id

* _Name:_ `get-accession-id`
* _Location:_ Same directory as transfers.py
* _Parameters:_ [`path`]
* _Return Code:_ 0
* _Output:_ Quoted value of the accession number (e.g. `"ID 42"`)

`get-accession-number` is run to customize the accession number of the created transfer. Its single parameter is the path relative to the transfer source location.  Note that no files are locally available when `get-accession-id` is run. It should print to standard output the quoted value of the accession number (e.g. `"ID42"`), `None`, or no output. If the return code is not 0, all output is ignored. This is POSTed to the Archivematica REST API when the transfer is created.

#### pre-transfer hooks

* _Parameters:_ [`absolute path`, `transfer type`]

All executable files found in `pre-transfer` are executed in alphabetical order when a transfer is first copied from the specified Transfer Source Location to the Archivematica pipeline. The return code and output of these scripts is not evaluated.

All scripts are passed the same two parameters:

* `absolute path` is the absolute path on disk of the transfer
* `transfer type` is transfer type, the same as the parameter passed to the script. One of 'standard', 'unzipped bag', 'zipped bag', 'dspace'.

There are some sample scripts in the pre-transfers directory that may be useful, or models for your own scripts.

* `00_file_to_folder.py`: If the transfer is a single file (eg a zipped bag or DSpace transfer), it moves it into an identically named folder. This is not required for processing, but allows other pre-transfer scripts to run.
* `00_unbag.py`: Repackages a bag as a standard transfer, writing md5 hashes from bag manifest into metadata/checksum.md5 file. This enables use of scripts such as add_metadata.py with bags, which would otherwise cause failure at the bag validation job.
* `add_metadata.py`: Creates a metadata.json file, by parsing data out of the transfer folder name.  This ends up as Dublin Dore in a dmdSec of the final METS file.
* `archivesspace_ids.py`: Creates an archivesspaceids.csv by parsing ArchivesSpace reference IDs from filenames.  This will automate the matching GUI if a DIP is uploaded to ArchivesSpace.
* `default_config.py`: Copies the included `defaultProcessingMCP.xml` into the transfer directory. This file overrides any configuration set in the Archivematica dashboard, so that user choices are guaranteed and avoided as desired.

#### user-input

* _Parameters:_ [`microservice name`, `first time at wait point`, `absolute path` , `unit UUID`, `unit name`, `unit type`]

All executable files in the `user-input folder` are executing in alphabetical order whenever there is a transfer or SIP that is waiting at a user input prompt. The return code and output of these scripts is not evaluated.

All scripts are passed the same set of parameters.

* `microservice name` is the name of the microservice awaiting user input. E.g. Approve Normalization
* `first time at wait point` is the string "True" if this is the first time the script is being run at this wait point, "False" if not. This is useful for only notifying the user once.
* `absolute path` is the absolute path on disk of the transfer
* `unit UUID` is the SIP or transfer's UUID
* `unit name` is the name of the SIP or transfer, not including the UUID.
* `unit type` is either "SIP" or "transfer"

There are some sample scripts in the pre-transfers directory that may be useful, or models for your own scripts.

* `send_email.py`: Emails the first time a transfer is waiting for input at Approve Normalization.  It can be edited to change the email addresses it sends notices to, or to change the notification message.

### Logs

Logs are written to a directory specified in the config file (or `/var/log/archivematica/automation-tools/` by default). The logging level can be adjusted, by modifying the transfers/transfer.py file. Find the following section and changed `'INFO'` to one of `'INFO'`, `'DEBUG'`, `'WARNING'`, `'ERROR'` or `'CRITICAL'`.

    'loggers': {
        'transfer': {
            'level': 'INFO',  # One of INFO, DEBUG, WARNING, ERROR, CRITICAL
            'handlers': ['console', 'file'],
        },
    },

### Multiple automated transfer instances

You may need to set up multiple automated transfer instances, for example if required to ingest both standard transfers and bags. In cases where hooks are the same for both instances, it could be achieved by setting up different scripts, each one invoking the transfers.py script with the required parameters. Example:

```
# first script invokes like this (standard transfer):
/usr/share/python/automation-tools/bin/python -m transfers.transfer --user <user>  --api-key <apikey> --ss-user <user> --ss-api-key <apikey> --transfer-source <transfer_source_uuid_for_std_xfers> --config-file <config_file>

# second script invokes like this (unzipped bags):
/usr/share/python/automation-tools/bin/python -m transfers.transfer --user <user>  --api-key <apikey> --ss-user <user> --ss-api-key <apikey> --transfer-source <transfer_source_2_uuid_for_bags> --config-file <config_file_2> --transfer-type 'unzipped bag'
```

`<config_file_1>` and `<config_file_2>` should specify different file names for db/PID/log files. See transfers.conf and transfers-2.conf in etc/ for an example

In case different hooks are required for each instance, a possible approach is to checkout a new instance of the automation tools, for example in `/usr/lib/archivematica/automation-tools-2`

### `transfer_async.py`

This is a new work-in-progress entry point similar to `transfers.transfer` that uses the new asynchronous endpoints of Archivematica being developed under the `/api/v2beta` API. It takes the same arguments, e.g.:

```
#!/usr/bin/env bash

cd /usr/lib/archivematica/automation-tools/

/usr/share/python/automation-tools/bin/python -m transfers.transfer_async \
  --user <user> --api-key <apikey> \
  --ss-user <user> --ss-api-key <apikey> \
  --transfer-source <transfer_source_uuid> \
  --config-file <config_file>
```

### Troubleshooting Automation Tools

1. Look for the sqlite db used by automation tools. It's path is available in `/etc/archivematica/automation-tools/transfers-std.conf`
2. Create a backup: `cp /var/archivematica/automation-tools/transfers-std.db{,.bkp}`
3. List current transfers

```
sqlite3  /var/archivematica/automation-tools/transfers-std.db
sqlite> select * from unit;
1|6c4db7f1-d4ae-40df-a5f1-ebecb7948060|archivematica_sip_419cdea4fc9e4f82bf7a7b779a1c1966|ingest|COMPLETE||0
2|b7e1010d-25c3-4873-aa99-ecf063de33ce|invalidPREMIStest|transfer|FAILED||0
3|e0bf1ae3-fa78-41a8-9fc1-8ad5349b2371|logs|transfer|PROCESSING||1
```

4. Remove the failed transfer:
```
sqlite> delete from unit where id=3;
sqite> .quit
```

