# Ydentic documentation metadataprocessor

## Introduction
This composite action is designed to process files so they can be used by Ydentic Ydocs.
Includes processing of the metadata header for .md files such as create date, updated date and authors.

## Setup

### Workflow
This action can be triggered from any github repository private and public with github external workflows enabled.

In your documentation repository create a folder named `.github` under this folder create another folder named `workflows`.
In this `workflows` folder create a filed named `workflow.yaml` (`workflow.yml` also works).
Copy this action template into that file.

```
name: 'Documentation metadata processing flow'

on: 
  push:
    branches:
      - master
      - releases/**

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Run build action
        uses: ydentic/ydocs-metadata-processor@v1.0.0
        with:
          github-author-name: <insert author name>
          github-author-email: <insert author email>
          github-token: ${{ secrets.GITHUB_TOKEN }}
          documentation-directory: <instert documentation folder (optional)>
```
- **IMPORTANT**: Replace `<insert author name>` with the name of a service account in github or just something recognizable for instance. "Developer" or "Documentation bot"
- **IMPORTANT**: Replace `<insert author email>` with the email of a service account in github or just something recognizable for instance. "developer@companyname.com" or "documentation-bot-@companyname.com"

- (Optional) You can change the name as you please this is not really important for the process but is required for the workflow creation.
- (Optional) You can edit the `branchs` property to anything you'd like for as long as it matches branch names in your documentation repo or the workflow wil not trigger.

- (Optional) You can replace `<instert documentation folder (optional)>` with the name of a folder inside the documentation repository that contains the documentation. For instance `Customer Manuals` otherwise remove the entire line from the file.

### Repository settings
As repository admin. Go to settings. And then under actions enable `Allow all actions and resusable workflows` en druk op `Save`.
![img/documentation-repo-action-settings](img/documentation-repo-action-settings.png)

## Reference

### Repository structure example
![img/documentation-repo-action-overview](img/documentation-repo-action-overview.png)

### Action parameter documentation

Branch definition
https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#using-filters



