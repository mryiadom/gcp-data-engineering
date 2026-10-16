# Setup notes

How the Google Cloud resources for this repo were created, in order.
Placeholders: PROJECT_ID is the project ID and BUCKET_NAME is the bucket name. Use your own values if you rebuild this.
Billing account IDs and credential files never go in this file.

## 1. Project, billing and budget

- Project created in the Console: project picker > New project.
  - Project name: GCP Data Engineering
  - Project ID: PROJECT_ID (pattern: gcp-de-portfolio-2026)
  - Location: No organisation
- Billing account linked to the project: Billing > Link a billing account.
- Budget: Billing > Budgets & alerts > Create budget.
  - Scope: this project only
  - Amount: £10 a month
  - Alerts at 50%, 90% and 100% of actual spend
  - A budget only sends alerts. It doesn't stop spending.

## 2. Command-line sign-in

The gcloud CLI was installed, then these were run in the terminal:

    gcloud init
    gcloud config set project PROJECT_ID
    gcloud auth application-default login
    gcloud auth application-default set-quota-project PROJECT_ID

Python signs in with Application Default Credentials. No service account key file is created.

## 3. APIs

BigQuery API and Cloud Storage API were already enabled, because Google enables them in new projects.
This was checked in the Console under APIs & Services > Enabled APIs & services.

## 4. Cloud Storage bucket

Created in the Console under Cloud Storage > Buckets > Create.

| Setting | Value |
|---|---|
| Name | payments-raw (BUCKET_NAME in the commands below) |
| Location | europe-west2 (London), location type Region |
| Default storage class | Standard |
| Public access prevention | Enforced |
| Access control | Uniform |
| Soft delete | 7 days (default) |
| Labels | project: payments, env: dev |

Command-line equivalent:

    gcloud storage buckets create gs://BUCKET_NAME --location=europe-west2 --default-storage-class=STANDARD --uniform-bucket-level-access --public-access-prevention

## 5. BigQuery datasets

Created in BigQuery Studio: Explorer > project > Create dataset.

| Dataset | Location | Holds |
|---|---|---|
| payments_raw | europe-west2 | Files loaded as they arrive |
| payments_staging | europe-west2 | Cleaned and typed copies of raw tables |
| payments_mart | europe-west2 | Fact and dimension tables for reporting |

Command-line equivalent (one per dataset):

    bq --location=europe-west2 mk --dataset PROJECT_ID:payments_raw

## 6. Checks

- Bucket, Configuration tab: Location type Region, Location europe-west2 (London), Default storage class Standard
- Bucket, Permissions tab: Public access "Not public", Access control "Uniform: No object-level ACLs enabled"
- payments_raw, Details tab: Data location europe-west2
- `gcloud config list`: project = PROJECT_ID
- Application Default Credentials file present (`Test-Path $env:APPDATA\gcloud\application_default_credentials.json` returns True)

All checks passed on 16 October 2026.
