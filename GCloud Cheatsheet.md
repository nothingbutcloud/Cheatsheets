# Environment Setup

Obtain `project_id` of your project:
```
gcloud config get-value project
```

View details of your project:
```
gcloud compute project-info describe --project $(gcloud config get-value project)
```

Setup default region and zone:
```
gcloud config set compute/region <region>
gcloud config set compute/zone <zone>
```

Setup common variables:
```
export PROJECT_ID=$(gcloud config get-value project)
export REGION=$(gcloud config get-value compute/region)
export ZONE=$(gcloud config get-value compute/zone)
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

# Compute Engine

Create a E2 standard virtual machine named `myvm`:
```
gcloud compute instances create myvm --zone $ZONE --machine-type e2-standard-2
```

Create a new persistant disk named `mydisk`:
```
gcloud compute disks create mydisk --size=200GB \
--zone $ZONE
```

Attach disk `mydisk` to Virtual Machine `myvm`:
```
gcloud compute instances attach-disk myvm --disk mydisk --zone $ZONE
```

Connect your VM with ssh:
```
gcloud compute ssh myvm --zone $ZONE
```


# GKE


# BigQuery
