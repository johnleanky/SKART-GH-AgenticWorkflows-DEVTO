---
name: New Day
description: Add the workflow run's UTC date to the website's Daily Updates navigation and dialog.
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Use the workflow run's UTC date to update `index.html` only.

First inspect every existing item in the Daily Updates navigation and every
existing daily update dialog. If the current UTC date is already represented by
a navigation control or dialog, preserve the file unchanged and call `noop`
with a short explanation.

Otherwise, edit `index.html` to:

1. Add the date to the existing Daily Updates navigation using the established
   ordinal date wording, HTML structure, classes, and arrow entity.
2. Add one matching accessible `<dialog>` that confirms the daily update ran.
   Follow the existing lowercase month-day ID convention and connect the
   navigation button to the dialog with `aria-controls`. Give the dialog unique
   matching `aria-labelledby` and `aria-describedby` IDs, retain the existing
   close-button pattern, and use the same date wording in its header.

Preserve every existing daily update and all unrelated content. Do not edit
`styles.css`, add scripts, or change the established styling. After making the
change, use the `create-pull-request` safe output to propose only `index.html`.