---
layout: docs
title:  "RAC Archivematica | Ingest"
---

## Automation Tools

To ingest a transfer using the automation tools, run a shell script from the Archivematica server that runs the automate transfer tool. The shell script calls `transfers/transfer.py` and passes arguments. `transfers/transfer.py` is used to prepare transfers, move them into the processing location, and take actions when user input is required.

Generally, a user will not need to call the script. A cron job has been set up to run the shell script that runs the automate transfer tool. This means that a script will watch a designated directory for a new transfer to ingest and will run the automated transfer script.

Only one transfer is sent to the pipeline at a time, the scripts wait until the current transfer is resolved (failed, rejected or stored as an AIP) before automatically starting the next available transfer.

Please see the administration page for more information on configuring the shell scripts that call `transfers/transfer.py`.

The script can be run from a shell window like:

```
user@host:/etc/archivematica/automation-tools$ sudo -u archivematica ./transfer-script.sh
```

When running, automated transfers stores its working state in a sqlite database.  It contains a record of all the transfers that have been processed.  In a testing environment, deleting this file will cause the tools to re-process any and all folders found in the Transfer Source Location.

The 2 scripts in the automation directory are `transfer-script-std-m.sh` and `transfer-script-unzbag-m.sh`.

## Manual Ingest

### Transfer and Ingest

1. In the **Transfer tab**, select the appropriate transfer type from the drop down menu. Enter the name of the transfer in the *Transfer name* field.

2. To select the transfer directory, click *Browse*. Select the directory to ingest into Archivematica, then click *Add*.

3. Click *Start Transfer*.

4. When *Job: Approve standard transfer*, appears on the screen, select *Approve transfer*.

5. Complete any microservice that requires human intervention. When *Micro-service: Create SIP from Transfer* has completed, proceed to the **Ingest tab**.

6. In in the **Ingest tab**, complete any microservice that requires human intervention. If a DIP will be created, in *Job: Upload DIP*, select *Upload DIP to ArchivesSpace* then follow the instructions in Manual Matching. Manual matching is not necessary if an ArchivesSpace IDs CSV file was included with the transfer.

### Manual Matching

1.  After selecting *Upload DIP to ArchivesSpace* in the **Ingest tab**, Archivematica loads a screen listing all ArchivesSpace resource records. Navigate to a specific collection either by searching for it or by navigating to it using the screen pager. To start mapping files in the DIP to resource components in a given collection, click the “Assign objects” button to the right of the collection title. To drill down to lower levels of the collection, click on the collection title.

2.  This opens the DIP object pairing screen which lists the objects in the DIP and Resources in ArchivesSpace to which the objects can be linked:

3.  Select one or more objects, then click on the appropriate resource. This action highlights the resource; to pair the objects with their resources, click on the “Pair” button on the top right of the screen or press Enter on your keyboard:

4.  Note that an object that has already been paired with a resource is greyed out and cannot be selected again, while a resource that has already been paired with an object changes font colour from black to red, but can still have more objects paired with it.

5.  Above, shown are pairs that have been created using this process. To delete a pair (i.e. make the digital object available to be linked to a different description), click the delete icon to the right of the pair. Once the mapping is completed, click “Save”. You will be asked to confirm the save, and then the mapping screen will close and you will be returned to the ingest tab in the Archivematica dashboard.

> Note:
> 
> * file names are sanitized during ingest--so if the original filename has spaces or special characters in it, they are now underscores--this affects filtering objects
> * filtering objects is not case sensitive
> * "select all" selects \*everything\*, not just files that are currently visible (i.e., filtered)

