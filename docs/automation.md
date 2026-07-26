# access automation

This folder contains automation for first-time access requests.

## Issue forms

- `.github/ISSUE_TEMPLATE/access-request.yml`

- Access template auto-applies type labels and the `pending` state label.

## Workflows

- `.github/workflows/validate-access-request.yml`
  - Trigger: request issue opened.
  - Loads access codes from the private `student-registry` repo.
  - Redacts the submitted access code immediately.
  - If invalid, comments, closes the issue, and marks it `failed`.
  - If valid, marks it `validated` and leaves the issue open for manual staff processing.

- `.github/workflows/process-request-label-actions.yml`
  - Manual `workflow_dispatch` workflow for access requests.
  - Processes all open `access-request` issues with the `validated` label.
  - Approves each by inviting requester to `student-requests`, posting next steps, and moving labels to `processed`.

## Required labels

Create these labels once in the destination repository:

- access-request
- pending
- validated
- failed
- approve
- reinvite
- reinvited
- processed

## Next implementation step

Current implementation status:

- access flow: validates access code on issue open, then staff runs a manual workflow to process validated requests.
- assignment flow runs in the private `student-requests` repository.

## Access code source

- The access code is stored in the private `student-registry` repo at `config/access-codes.json`.
- All workflows in this repository use one secret: `COURSE_AUTOMATION_TOKEN`.
