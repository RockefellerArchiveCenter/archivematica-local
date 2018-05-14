## Uploading PDF Digital Objects to DIMES Post-Ingest

Once the DIP Upload process has completed in Archivematica, log into the RACIMAGES server (192.168.50.35) using your username and password.

From your home directory run the script to move objects, passing in the DIP URI as the first argument.

You will be prompted to enter your sudo password for the RACIMAGES server


You will then be prompted to enter the password for archivesuser on the Archivematica server (192.168.50.108)


The terminal will log the directory being accessed, as well as each file as it is copied from the Archivematica DIP server to /var/tmp directory on the RACIMAGES server.

Once this process has completed, a script
(/home/harnold/makePDFthumb.sh) set to run automatically will do the following:

-   Make a thumbnail for display purposes based on the first page of the PDF

-   Move the thumbnail and PDF to /var/www, then change their permissions so they are web accessible