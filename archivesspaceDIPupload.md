# Archivematica/ArchivesSpace DIP Upload

## CSV Structure

CSV for automated matching
--------------------------

At this stage, you can create a CSV to match files with their parent components in ArchivesSpace. There should be one CSV per SIP, with the filename "archivesspaceids.csv" in the /metadata directory. The first column contains the filenames and the second column contains the refid of the component the file needs to be linked to.There is no header row.

Note that filenames, including file extensions, are case sensitive, and should contain the full path. If files were manually normalized, the filepath should be for the original filename, not the file in the
/access directory.

For example:

  data/objects/Youth Organizations.doc   ref5086\_rts
  -------------------------------------- --------------



## Manual Matching

\*\*\*file names are sanitized during ingest--so if the original filename has spaces or special characters in it, they are now underscores--this affects filtering objects

\*\*\*filtering objects is not case sensitive

\*\*\*"select all" selects \*everything\*, not just files that are currently visible (i.e., filtered)

1.  At the DIP upload micro-service in the Archivematica dashboard, the user can choose to upload the DIP to ArchivesSpace. Archivematica then loads a screen listing all ArchivesSpace resource records.
    > The user navigates to a specific collection either by searching for it or by navigating to it using the screen pager. To start mapping files in the DIP to resource components in a given collection, the user clicks the “Assign objects” button to the right of the collection title. To drill down to lower levels of the collection, the user clicks on the collection title.

2.  This opens the DIP object pairing screen which lists the objects in the DIP and Resources in ArchivesSpace to which the objects can be linked:

3.  The user selects one or more objects, then clicks on the appropriate resource. This action highlights the resource; to pair the objects with their resources, click on the “Pair” button on the top right of the screen or press Enter on your keyboard:

4.  Note that an object that has already been paired with a resource is greyed out and cannot be selected again, while a resource that has already been paired with an object changes font colour from black to red, but can still have more objects paired with it.

5.  Above, shown are pairs that have been created using this process. To delete a pair (i.e. make the digital object available to be linked to a different description), click the delete icon to the right of the pair. Once the mapping is completed, click “Save”. You will be asked to confirm the save, and then the mapping screen will close and you will be returned to the ingest tab in the Archivematica dashboard.


## Configuration
Before ingesting digital objects destined for ArchivesSpace, ensure that the ArchivesSpace DIP upload settings in the administration tab of the dashboard have been set.

These settings should be created and saved before digital objects destined for upload to ArchivesSpace are processed. Note that these can be set once and used for processing any number of transfers (i.e. they do not need to be re-set for each transfer). In order to save changes to the ArchivesSpace DIP upload configuration, you must enter the password before clicking save. Note that Archivematica will *not* show you an error if the password is not entered.

## Data mapping

### Basic information

Title: Derive from original filename of digital object.
Identifier: Populate with Archivematica DIP URI without digital object filename. 
Publish: Set as TRUE or FALSE based on PREMIS statement (see Publish: Base on PREMIS below). 
Type: Populate with value from Object Type field in Archivematica administration settings. If no data entered in this field, leave empty.
Language: Derive from parent component in ArchivesSpace.
Restrictions?: Set as TRUE or FALSE based on PREMIS statement (see Restrictions: Base on PREMIS below).

### File Version

File URI: Populate with URL prefix from URI Prefix field in  Archivematica administration settings, plus file UUID and filename, for example: http://storage.rockarch.org/[UUID]-filename. 
Use Statement: Populate with value from Use Statement field in Archivematica administration settings. 
XLink Attribute Actuate: Derive from PREMIS statement (see Restrictions: Base on PREMIS below). If no PREMIS statements are present, base on value from XLink Attribute Actuate field in Archivematica administration settings. 
XLink Show Attribute: Derive from PREMIS statement (see Restrictions: Base on PREMIS below). If no PREMIS statements are present, base on value from XLink Show Attribute field in Archivematica administration settings.
File Format Name: Populate with DIP digital object file format name as identified by Archivematica. 
File Format Version: Populate with DIP digital object file format version as identified by Archivematica.
File Size: Populate with DIP digital object file size measured in bytes, as identified by Archivematica. 

### Notes

Conditions Governing Access note: Derive from PREMIS <rightsGrantedNote> (see Restrictions: Base on PREMIS below). If there is no content in <rightsGrantedNote>, populate with value from Conditions Governing Access field in Archivematica administration settings. If no data is entered in this field, do not add note. 
Conditions Governing Use note: Derive from PREMIS <rightsGrantedNote> (see Restrictions: Base on PREMIS below). If there is no content in <rightsGrantedNote>, populate with value from Conditions Governing Use field in Archivematica administration settings. If no data is entered in this field, do not add note.
Existence and Location of Originals note: automatically populate with Archivematica AIP UUID 
If specified in administration settings, Any other notes attached to the parent component in ArchivesSpace should also be attached to the digital object record.

### Agents

Any agents linked to the parent component in ArchivesSpace should be linked to the digital object record, if specified in administration settings.
Agent records for agents recorded in Archivematica should be created and linked to the digital object record, if specified in administration settings.
Subjects
Any subjects linked to the parent component in ArchivesSpace should be linked to the digital object record, if specified in administration settings.
Record Link
Create link to parent component in ArchivesSpace

## Restrictions: Base on PREMIS

### Disseminate

If PREMIS <act> = Disseminate and PREMIS <restriction> = Allow, Restrictions? = FALSE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Conditional, Restrictions? = TRUE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Disallow, Restrictions? = TRUE
If PREMIS <act> = Disseminate, populate Conditions Governing Access note with contents of PREMIS rightsGrantedNote
When Restrictions?=TRUE, both XLink Attribute Actuate and XLink Attribute Show will be set to “none.”

### Publish

If PREMIS <act> = Publish, populate ConditionsGoverningUse with contents of PREMIS rightsGrantedNote

## Publish: Base on PREMIS

If PREMIS <act> = Disseminate and PREMIS <restriction> = Allow, Publish = TRUE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Conditional, Publish = FALSE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Disallow, Publish = FALSE
