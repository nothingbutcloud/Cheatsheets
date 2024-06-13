# Environment Setup

Setup default region and zone:
```
gcloud config set compute/region <region>
gcloud config set compute/zone <zone>
```

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

# IAM

Obtain an authorization token using your account:
```
gcloud auth print-access-token
```

# Calling Google REST API

Call API with Bearer Authorization Token
```
curl -s \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  <api_url> \
  <api_params>
```

# Cloud Storage

Download files to current directory:
```
gcloud storage cp gs://path/to/file .
```
or
```
gsutil cp -r gs://path/to/file .
```

Upload files to Cloud Storage:
```
gsutil cp local_file gs://bucket_name
```


# GKE


# BigQuery
