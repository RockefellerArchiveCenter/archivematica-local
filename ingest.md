---
layout: docs
title:  "Ingest"
---

## Manual Ingest

### Transfer and Ingest

1. In the **Transfer tab**, select the appropriate transfer type from the drop down menu. Enter the name of the transfer in the *Transfer name* field.

2. To select the transfer directory, click *Browse*. Select the directory to ingest into Archivematica, then click *Add*.

3. Click *Start Transfer*.

4. When *Job: Approve standard transfer*, appears on the screen, select *Approve transfer*.

5. Complete any microservice that requires human intervention. When *Micro-service: Create SIP from Transfer* has completed, proceed to the **Ingest tab**.

6. In in the **Ingest tab**, complete any microservice that requires human intervention. If a DIP will be created, in *Job: Upload DIP*, select *Upload DIP to ArchivesSpace* then follow the instructions in Manual Matching.

### Manual Matching

1.  After selecting *Upload DIP to ArchivesSpace* in the **Ingest tab**, Archivematica loads a screen listing all ArchivesSpace resource records. Navigate to a specific collection either by searching for it or by navigating to it using the screen pager. To start mapping files in the DIP to resource components in a given collection, click the “Assign objects” button to the right of the collection title. To drill down to lower levels of the collection, click on the collection title.

2.  This opens the DIP object pairing screen which lists the objects in the DIP and Resources in ArchivesSpace to which the objects can be linked:

3.  Select one or more objects, then click on the appropriate resource. This action highlights the resource; to pair the objects with their resources, click on the “Pair” button on the top right of the screen or press Enter on your keyboard:

4.  Note that an object that has already been paired with a resource is greyed out and cannot be selected again, while a resource that has already been paired with an object changes font colour from black to red, but can still have more objects paired with it.

5.  Above, shown are pairs that have been created using this process. To delete a pair (i.e. make the digital object available to be linked to a different description), click the delete icon to the right of the pair. Once the mapping is completed, click “Save”. You will be asked to confirm the save, and then the mapping screen will close and you will be returned to the ingest tab in the Archivematica dashboard.

>\*\*\*file names are sanitized during ingest--so if the original filename has spaces or special characters in it, they are now underscores--this affects filtering objects
>
>\*\*\*filtering objects is not case sensitive
>
>\*\*\*"select all" selects \*everything\*, not just files that are currently visible (i.e., filtered)

## Ingest Using Automation Tools

To ingest a transfer using the automation tools, run a shell script that runs the automate transfer tool. The shell script calls `transfers/transfer.py` and passes arguments. `transfers/transfer.py` is used to prepare transfers, move them into the pipelines processing location, and take actions when user input is required.

Generally, a user will not need to call the script. A cron job has been set up to run the shell script that runs the automate transfer tool.

Only one transfer is sent to the pipeline at a time, the scripts wait until the current transfer is resolved (failed, rejected or stored as an AIP) before automatically starting the next available transfer.

Please see the administration page for more information on configuring the shell scripts.


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
