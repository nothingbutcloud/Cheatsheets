# GCloud Cheatcsheet

## Environment Setup

Setup common variables:
```
export PROJECT_ID=`gcloud config get-value project`
export REGION=
export ZONE_ID=
```

Alernative way:
```
export PROJECT_ID=$(gcloud config list --format 'value(core.project)')
export PROJECT_NUMBER=$(gcloud projects list --filter=projectId:$PROJECT_ID \
  --format="value(projectNumber)")
```
