---
layout: docs
title:  "RAC Archivematica | Updating"
---

## Upgrading to a new release of Archivematica

### 1. Review Release Notes (Archivematica Product Owner)

Review release notes made available on Archivematica wiki, noting any changes that may impact RAC workflows or the upgrade process. If skipping versions (e.g., from 1.7 to 1.9), review release notes for intermediate versions.

### 2. Plan Upgrade (Archivematica Product Owner)

Coordinate with Artefactual, RAC Information Systems Manager, and other key [RAC staff](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) to plan upgrade at least 3 weeks in advance. Production and development upgrade should be planned at the same time, with production scheduled for 2 weeks after development. The upgrade schedule will likely look like:

* Week 1: Upgrade development (Artefactual)
* Week 2: Upgrade integrated applications, test development (RAC)
* Week 3: Upgrade production (Artefactual)
* Week 4: Upgrade integrated applications, test production (RAC)

### 3. Set up Development VMs (Information Systems Manager) (optional)

This is only necessary if the Archivematica upgrade involves a move to new VMs. This step includes:

* Setting up dev VMs in accordance with [current specs](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/)
* Setting up ssh access for [select RAC staff](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) for VMs
* Setting up all accounts and access for Artefactual
* Configuring [DNS](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/

When this is complete, convey information about IPs and logins to the Archivematica Product Owner so that she can update the Archivematica Info Sheet, inform key staff, and let Artefactual know our development environment is ready to be upgraded.

### 4. Upgrade (Artefactual)

Archivematica Product Owner alerts key staff to window where Archivematica development environment will be down. Artefactual upgrades both pipelines and the storage service in our dev environment.

### 5. Update Integrated Applications in Development Environment (Archivematica Product Owner)

Review whether user accounts, API Keys, and Pipeline and Location UUIDs have changed, and work with key staff to update configs in other applications as necessary. Connected applications may include Fornax and Gemini. Ensure that Storage Service callbacks for Gemini are [properly configured](https://github.com/RockefellerArchiveCenter/gemini/blob/base/README.md#archivematica-configuration).

### 6. Test on Development (Archivematica Product Owner)

Along with key staff, test the following:

* All expected [user accounts](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) are present
* Transfers can be sent to and stored in all locations on both pipelines
* All integrations work as expected
* Processing configurations are set up as expected

Errors as they occur will be communicated to the Archivematica Product Owner, who will work with Artefactual to resolve them. When testing is complete, the Archivematica Product Owner will alert Artefactual and the Information Systems Manager.

### 7. Upgrade (Artefactual)

Archivematica Product Owner alerts key staff to window where Archivematica production environment will be down. Artefactual upgrades both pipelines and the storage service in our production environment.

### 8. Update Integrated Applications (Archivematica Product Owner)

Review whether user accounts, API Keys, and Pipeline and Location UUIds have changed, and work with key staff to update configs in other applications as necessary. Connected applications may include Fornax and Gemini. Ensure that storage service callbacks for Gemini are [properly configured](https://github.com/RockefellerArchiveCenter/gemini/blob/base/README.md#archivematica-configuration).

### 9. Test on Production (Archivematica Product Owner)

Along with key staff, test the following:

* All expected [user accounts](https://docs.rockarch.org/systems-info-sheets/archivematica-info-sheet/) are present
* Transfers can be sent to and stored in all locations on both pipelines
* All integrations work as expected
* Processing configurations are set up as expected

Errors will be reported to the Archivematica Product Owner, who will work with Artefactual to resolve them. When testing is complete, the Archivematica Product Owner will alert Artefactual and key staff.
