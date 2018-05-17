---
layout: docs
title:  "Appendix"
---

## PREMIS Mapping

### Restrictions: Base on PREMIS

### Disseminate

If PREMIS <act> = Disseminate and PREMIS <restriction> = Allow, Restrictions? = FALSE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Conditional, Restrictions? = TRUE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Disallow, Restrictions? = TRUE
If PREMIS <act> = Disseminate, populate Conditions Governing Access note with contents of PREMIS rightsGrantedNote
When Restrictions?=TRUE, both XLink Attribute Actuate and XLink Attribute Show will be set to “none.”

### Publish

If PREMIS <act> = Publish, populate ConditionsGoverningUse with contents of PREMIS rightsGrantedNote

### Publish: Base on PREMIS

If PREMIS <act> = Disseminate and PREMIS <restriction> = Allow, Publish = TRUE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Conditional, Publish = FALSE
If PREMIS <act> = Disseminate and PREMIS <restriction> = Disallow, Publish = FALSE