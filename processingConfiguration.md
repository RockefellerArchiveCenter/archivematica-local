---
layout: docs
title:  "Processing Configuration"
---

### Processing configuration

On the processing configuration page of the Administration tab, it is possible to automate steps.

These should be the default settings for processed born digital materials:

|  Step                                                                          |  Check |  Action |
|  --------------------------------------------------------------------------------- |----------- | --------------------------|
|  Send transfer to quarantine                                                      | ✓ |  No |
|  Approve normalization                                                            | ✓ | Yes |
|  Store AIP                                                                        |   | n/a |
|  Transcribe files (OCR)                                                           | ✓ | No |
|  Generate transfer structure report                                               | ✓ | Yes |
|  Remove from quarantine after \_\_ days                                           |   | n/a |
|  Create SIP(s)                                                                    | ✓ | Create single SIP and continue processing |
|  Extract packages                                                                 | ✓ | No |
|  Normalize                                                                        | ✓ | Normalize for preservation and access |
|  Reminder: add metadata if desired                                                |   | n/a |
|  Examine contents                                                                 | ✓ | Skip examine contents |
|  Select file format identification command (Transfer)                             | ✓ | Fido version 1 PUID |
|  Select file format identification command (Ingest)                               | ✓ | Use existing data |
|  Select file format identification command (Submission documentation & metadata)  | ✓ | File extension |
|  Delete packages after extraction                                                 | ✓ | Yes |
|  Select compression algorithm                                                     | ✓ | 7z using bzip2 |
|  Select compression level                                                         | ✓ | 5 - normal compression mode |
|  Store AIP location                                                               | ✓ | Store AIP in standard Archivematica directory |
|  Store DIP location                                                               | ✓ | Store DIP in standard Archivematica directory |
