---
layout: docs
title:  "RAC Archivematica | Workflows by Content Type"
---

## Digitized Materials

### Special Projects

1. Run script(s) created for special project to structure transfer and generate `rights.csv` and `archivesspaceids.csv`. [Rockefeller Foundation Officers' Diary Example](https://github.com/RockefellerArchiveCenter/scripts/blob/master/archivematica/generateRfodSip.py)

2. Move transfer to the IngestQueue directory in the Transfer Source.

3. Ingests happen automatically overnight with a cron job running [startTransfer.py](https://github.com/RockefellerArchiveCenter/scripts/blob/master/archivematica/startTransfer.py) pointed at the IngestQueue directory.

### On Demand

1. Run [generateDigitizationSip.py](https://github.com/RockefellerArchiveCenter/scripts/blob/master/archivematica/generateDigitizationSip.py) with the -a flag to create a [structured directory](transferAndSetup#transfer-structure) and [ArchivesSpace IDs CSV file](transferAndSetup#archivesspace-ids-csv). Include the -c flag if citation sheets need to be removed.

2. Run [premisCsvDigitization.py](https://github.com/RockefellerArchiveCenter/scripts/blob/master/archivematica/premisCsvDigitization.py) to create the [PREMIS rights CSV file](transferAndSetup#transfer-structure#premis-csv).

3. Move transfer to Transfer Source.

4. Run [startTransfer.py](https://github.com/RockefellerArchiveCenter/scripts/blob/master/archivematica/startTransfer.py) with the list of transfers to start.

## Legacy Born Digital

*In development.*

## Audiovisual

*In development.*