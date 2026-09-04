---
name: Weekly Report Status
description: Publish a concise weekly report of repository commits, issues, and pull requests.
engine: copilot
on:
  schedule: weekly on monday
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Create a concise repository activity report for the seven-day period ending at
the workflow start time, using UTC timestamps. Use `gh` to inspect commits,
issues, and pull requests in the current repository.

Publish exactly one new issue through the `create-issue` safe output. Give it a
clear title after the configured prefix and structure its body with `### Summary`,
`### Commits`, `### Issues`, `### Pull Requests`, and `### Reporting Window`
sections. Include useful counts and brief links or descriptions for notable
activity while avoiding `@` mentions.

If no commits, issue activity, or pull request activity occurred during the
reporting window, still publish the issue and clearly state that no activity
occurred. Do not infer activity outside the defined window.