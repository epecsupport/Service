---
layout: default
title: Inventor Model Standards
autolink: true
---

# Support/Tech Services Model Standards:

## Fasteners:
- When possible, demote fastener groups for re-use (see: Fastener Groups).
- Import McMaster models wherever possible rather than Content Center models.
- Add bolt length behind McMaster number (i.e., 91247A724_3in_Medium-Strength Grade 5 Steel Hex Head Screw.ipt)
- Store in proper fastener folder.

### Fastener Groups
- Convert fractional bolt sizes to decimal - Windows does not allow / in the filename (i.e., 3/8" = .375).
- Standardize file name as "Fastener Group, %Type% %Size%-%TPI%x%Length% %Gap% spacing.iam
- See type abbreviations below, a typical bolt stack would be CFFLN.  A stack into a threaded hole would be CFL
- Store in proper fastener folder.
- A typical entry would be, "Fastener Group, CFFLN .5-13x2.75 1.75 spacing.iam"  This indicates a bolt, flat, flat, lock, nut arrangement in 1/2"-13, 2.75" bolt length holding a 1.75" joint.

### Type Abbreviations:
- C: Capscrew
- F: Flat washer
- L: Lock washer
- N: Nut

## General:
