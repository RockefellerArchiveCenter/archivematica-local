### Exporting files from FTK

1.  Setup - directories

    a.  Create a directory where everything will get exported

    b.  Create subdirectories for each grouping. The names should easily
        > identify what materials will be in the directory (e.g.,
        > "unrestricted-ms-office", "organization-records-spend-down-2023")

    c.  In each directory, create two subdirectories:

2.  Setup - FTK

    a.  You can use the "filter" functionality to only view files that
        > have been bookmarked and do not have a label (or have a
        > specific label). There is a filter called
        > "Archivematica-export"

    b.  In order to edit an existing filter or create a new one, go to
        > Manage → Filters → Manage Filters.

    c.  There is a "Bookmarked" filter that comes with FTK. There is
        > also a custon "Archivematica-export" filter for files that are
        > bookmarked but do not have a label. It should have the
        > following properties:

        i.  Bookmark | Is a Member of | \[Any Bookmark\]

        ii. Label | Attribute Does Not Exist

3.  Export files

    a.  Export files that are not labeled

        i.  Navigate to the Overview tab

        ii. Filter → Tab Filter…

        iii. Choose Archivematica-export from dropdown menu and click
            > okay

        iv. Export all files

            1.  File items → Unchecked Items (assuming all items
                > are unchecked)

            2.  Go to File → Export

            3.  The "Export" window will appear

                a.  File options

                    i.  Uncheck "Limit path length"

                    ii. Check "Create manifest files"

                b.  Items to Include

                    i.  All listed

                c.  Destination base path:

                    i.  Select the appropriate directory

        v.  Export files by format (may be needed for manual
            > normalization workflow)

            1.  Expand "File Category"

            2.  Expand further categories as needed

            3.  When you have selected the category of files that you
                > want to export, go to File → Export

            4.  The "Export" window will appear

                a.  File options

                    i.  Uncheck "Limit path length"

                    ii. Check "Create manifest files"

                b.  Items to Include

                    i.  All listed

                c.  Destination base path:

                    i.  Select the appropriate directory

    b.  Export files by label

        i.  Navigate to the Overview tab

        ii. Filter → Tab Filter…

        iii. Choose Bookmarked from the dropdown menu and click okay

        iv. Expand "Labels"

        v.  When you have selected the label that you want to export, go
            > to File → Export

        vi. The "Export" window will appear

            1.  File options

                a.  Uncheck "Limit path length"

                b.  Check "Create manifest files"

            2.  Items to Include

                a.  All listed

            3.  Destination base path:

                a.  Select the appropriate directory

4.  Group exported files\
    > \*\*\*I wrote a shell script that does all of this automatically

    a.  FTK will create a new directory called "1" and a file
        > "FTKExportSummary1.txt" in the destination base path that
        > you provided.

    b.  Rename "1" to "objects"

    c.  Create a "metadata" directory with the subdirectory
        > "subsmissionDocumentation." Move "FTKExportSummary1.txt" to
        > /metadata/submissionDocumentation

5.  The directory should look like:

  --------------------------
  /top-level

  /objects

  file1.doc

  file2.docx

  file3.pdf

  /metadata

  /submissionDocumentation

  FTKExportSummary1.txt
  --------------------------
  --------------------------