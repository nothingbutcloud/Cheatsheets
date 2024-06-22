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

Enable Google APIs (For Vertax AI):
```
gcloud services enable \
  compute.googleapis.com \
  iam.googleapis.com \
  iamcredentials.googleapis.com \
  monitoring.googleapis.com \
  logging.googleapis.com \
  notebooks.googleapis.com \
  aiplatform.googleapis.com \
  bigquery.googleapis.com \
  artifactregistry.googleapis.com \
  cloudbuild.googleapis.com \
  container.googleapis.com
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

# Network

Create new network:
```
gcloud compute networks create labnet --subnet-mode=custom
```

Create subnet:
```
gcloud compute networks subnets create labnet-sub \
   --network labnet \
   --region $REGION \
   --range 10.0.0.0/28
```

Create firewall rule:
```
gcloud compute firewall-rules create labnet-allow-internal \
	--network=labnet \
	--action=ALLOW \
	--rules=icmp,tcp:22 \
	--source-ranges=0.0.0.0/0
```


# GKE

Create a GKE cluster:
```
gcloud container clusters create --machine-type=e2-medium --zone=$ZONE lab-cluster
```

Authenticate with the GKE cluster:
```
gcloud container clusters get-credentials lab-cluster
```

Create a new Deployment `hello-server` from the sample container image:
```
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
```

Expose the service:
```
kubectl expose deployment hello-server --type=LoadBalancer --port 8080
```

# Cloud SQL

Connect to your instance:
```
gcloud sql connect myinstance --user=root
```


# BigQuery


# AI

Bulk update cloud storage path of data csv file.
```
sed -i -e "s/original_path/${BUCKET}/g" ./data.csv
```
