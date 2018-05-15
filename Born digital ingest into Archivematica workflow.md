---
layout: docs
title:  "Born digital ingest into Archivematica workflow"
---

The purpose of this guide is to detail the Archivematica Ingest workflow for processed born digital materials. Processed digital materials are digital objects that have been described in a finding aid.


## Step 1: Export files & group into SIPs


### ArchivesSpace DIP Upload Administrative Settings

More information can be found at
[*https://www.archivematica.org/en/docs/archivematica-1.4/user-manual/access/archivists-toolkit/\#administrative-settings*](https://www.archivematica.org/en/docs/archivematica-1.4/user-manual/access/archivists-toolkit/#administrative-settings)

-   ArchivesSpace host, backend port, administrative user, password, URL prefix, and repository number will generally not change

-   Restrictions apply should be set to "base on PREMIS"

-   XLink Actuate - on request

-   XLink show - embed

-   Use statement: must be from controlled list in ArchivesSpace

-   Object type: must be from controlled list in ArchivesSpace

-   Conditions governing access:

-   Conditions governing use:

### PREMIS Agent

This should be:

Agent Identifier Value: NNttR

Agent Name: Rockefeller Archive Center

Step 4: Transfer to Archivematica & create SIP
==============================================

Overview
--------

The ingest of files through Archivematica into our storage system involves several steps. The first step is the Transfer process, which transforms any set of digital objects and/or directories into a SIP
(Submission Information Package). In the Transfer tab of the Dashboard,
the user selects digital objects from Staging (Y: drive 192.168.50.42)
to copy into Archivematica. Once uploaded to the dashboard, transfers run through several micro-services:

-   UUID assignment, checksum verification (if checksums are present)

-   package extraction (i.e. unzipping of zipped or otherwise packaged files)

-   virus checking

-   indexing

-   format identification and validation; and metadata extraction.

At the end of transfer, the user creates a SIP from one or more transfer(s). Once this is done, the SIP is moved into ingest.

This work primarily takes place in the "transfer" tab

Note: Once this process begins, you cannot go back to earlier stages and reconfigure ingest options. The system will pause at certain decision-making points and prompt for input prior to continuing. It’s best to be prepared for the entire process at the start, for example,
know if normalization is required, have rights statements prepared, etc.
