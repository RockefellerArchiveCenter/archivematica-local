---
layout: docs
title:  "RAC Archivematica | Workflows by Content Type"
---

## Digitized Materials

1. Run `generateDigitizationSip.sh` to create a [structured directory](transferAndSetup#transfer-structure).
	Uses RefId, entered while interacting with the script, to create an Archivematica-ready transfer with the name archivematica_sip_<refid>, and put files from the (1) Master, (1) Master Edited and (1) Service Edited directories into the transfer directory.

2. Run `archivesSpaceCsvDigitization.py` to create the [ArchivesSpace IDs CSV file](transferAndSetup#archivesspace-ids-csv).
	Uses RefId to find transfer directory created in the above step, then creates a CSV file with access file names in one column and RefId in the other column. This is the ArchivesSpace automated DIP matching CSV.

3. Run `premisCsvDigitization.py` to create the [PREMIS rights CSV file](transferAndSetup#transfer-structure#premis-csv).
	Uses RefId to find transfer directory then creates a CSV to record PREMIS rights information for each file. How much this script requires user input and how much it pulls from stored rights is TBD.

4. Move transfer to Transfer Source.
	Will be an automated process, details TBD

5. Automation tools cron job starts transfer


## Born Digital

*In development.*

## Audiovisual

*In development.*