# Manual Ingest with Archivematica Dashboard

The purpose of this guide is to detail the Archivematica Ingest workflow for processed digital materials. Processed digital materials are digital objects that have been described in a finding aid. These materials may be either digitized or born-digital. The workflow for unprocessed material and born-digital materials will be incorporated (and finalized)
at a later point.

Prior to working with Archivematica, bagged materials should be validated and evaluated using quality control measures. A pre-ingest workflow is provided to outline the steps needed to ensure data is transferred safely prior to ingest.

The ingest of files through Archivematica into our storage system involves several steps. The first step is the Transfer process, which transforms any set of digital objects and/or directories into a SIP
(Submission Information Package). In the Transfer tab of the Dashboard,
the user selects digital objects from Staging (Y: drive 192.168.50.42)
to copy into Archivematica. Once uploaded to the dashboard, transfers run through several micro-services: UUID assignment, checksum verification (if checksums are present); package extraction (i.e.
unzipping of zipped or otherwise packaged files); virus checking;
indexing; format identification and validation; and metadata extraction.
At the end of transfer, the user creates a SIP from one or more transfer(s). Once this is done, the SIP is moved into ingest.

During ingest, digital objects are run through several additional micro-services, including normalization, which packages the SIP into an AIP (Archival Information Package) and generates access copies that are then packaged into a DIP (Dissemination Information Package). PREMIS rights information is added to the SIP during ingest. The UUIDs and filenames of the DIPs are then matched to the appropriate components in the Archivists’ Toolkit (aka ATReference).\
**\

## Creating a transfer

1.  In the transfer tab, select your transfer type in the dropdown menu. Transfer types currently used at the RAC include standard, unzipped bag, and zipped bag. See the Transfer Structure Documentation for instructions on how to structure each transfer type.

1.  **Transfer name**. TBD

2.  **Accession number.** Complete this field with the accession number(s) of the materials. The accession number should be separated by a `.` . Leave blank if the accession number is not known, or if the transfer includes files from multiple accessions.
	
3.  In the transfer tab, browse to the Staging area to select the set of digital objects for upload.

4.  Once the digital object directory has been uploaded, select the **Start Transfer** button to start the transfer process.

## Processing the transfer

1.  In the dashboard transfer tab, the transfer will appear in the dashboard with a bell icon next to its name. This means that it is awaiting a decision by the user. In the Actions drop-down menu, select **Approve transfer** to begin processing the transfer. You may also **Reject transfer** to quit processing. 

3.  The actions for the microservices tab should be automated by selecting the proper options in the Processing Configuring section of the Administration tab.

## Create SIP

1.  Once the transfer has been transformed into a SIP, the Ingest tab will show a number signifying that there’s a new SIP available for processing. Click on the Ingest tab to view the SIP and continue ingest.

3.  The actions for the microservices tab should be automated by selecting the proper options in the Processing Configuring section of the Administration tab.'

1.  Once normalization is complete the user can review the results in the normalization report. Click on the **report** icon next to the Actions drop-down menu (highlighted in yellow below).

2.  If nothing has failed in the Normalization Report, click **Review** to see the files that were created. Depending on the format type, files can either be reviewed in the browser or downloaded for review.

3.  Select **Approve normalization** in the Action drop-down menu to continue processing the SIP. You can also **Reject the SIP** or **re-do** normalization. If there are errors in normalization, follow the instructions in [Error handling](https://www.archivematica.org/wiki/UM_error_handling) to learn more about the problem. Contact the Head of Digital Programs.

1.  Entirely automatic micro-services

    a.  Verify SIP compliance

    b.  Verify transfer compliance

    c.  Rename SIP directory with SIP UUID

    d.  Include default SIP processingMCP.xml

    e.  Remove cache files

    f.  Clean up names

2.  Normalize

    a.  If you want to create a DIP, you \*must\* select "Normalize for access" or "Normalize for preservation and access." This includes cases when files will not be migrated. A DIP will only be created if there is an /access directory.

    b.  If you are manually normalizing before transfer to Archivematica, and have /access and /preservation as subdirectories in /manualNormalization, select "Normalize for preservation and access." Do not select "Normalize manually" if you manually normalized before transfer.

3.  After normalization, a Reminder to add metadata if desired should appear. At this point, again click the template icon for the SIP you are processing.

    a.  Under Metadata, click "Manual Normalization Event Detail."
        > Review what is listed and add information if needed.

    b.  Review other metadata and rights information

    c.  After reviewing metadata, return to the Ingest tab and click
        > "Continue" for "Reminder: Add metadata if desired"

4.  After normalization is approved, the SIP runs through a number of micro-services, including processing of the submission documentation, generation of the METS file, indexing, generation of the DIP and packaging of the AIP. When these micro-services are complete, you can upload the DIP and store the AIP.


## Store AIP
After normalization is approved, the SIP runs through a number of micro-services, including processing of the submission documentation,
generation of the METS file, indexing, generation of the DIP and packaging of the AIP. When these micro-services are complete, you can upload the DIP and store the AIP.

If desired, review the contents of the AIP in another tab by clicking on **Review**. More information on the [AIP structure](https://www.archivematica.org/wiki/AIP_structure) and the
[METS/PREMIS](https://www.archivematica.org/wiki/METS) file is available on the Archivematica wiki.

Select **Store AIP** to move the AIP into archival storage.

## Upload DIP

1.  Click "Upload DIP to ArchivesSpace" in the drop down menu for "Job:
    > Upload DIP"

2.  Click on the template icon in "Job: Choose Config for ArchivesSpace DIP Upload" to be brought to the page to match DIP objects to the resource.

3.  Click "ArchivesSpace Config" in the drop down menu for "Job: Choose Config for ArchivesSpace DIP Upload."
