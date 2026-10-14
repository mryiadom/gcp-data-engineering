# Card payments monitoring

A card issuer's daily spending view and first line of fraud rules, built on Google Cloud.

**Status:** Week 1 of 9 (scaffold and environment). Nothing below "Planned" exists yet.

## What it will do

Synthetic card transactions are generated in Python with Faker, landed in Cloud Storage, loaded into partitioned BigQuery tables in `europe-west2` (London), and modelled in Dataform into a star schema and rule-based alerts, with assertions at each layer. All data is synthetic. No real customer or card data is used.

## Planned

| Week | Deliverable |
|------|-------------|
| 2 | Synthetic card-transaction generator in Python |
| 3 | Loads to Cloud Storage and partitioned BigQuery tables |
| 4 | Dataform staging models, assertions and a first mart |
| 5 | Star schema with a data model diagram |
| 6 | Incremental loads that handle duplicates and late data |
| 7 | Transaction monitoring rules built with window functions |
| 8 | pytest suite and CI on every pull request |
| 9 | Architecture diagram, sample outputs, production notes |

## Set up the environment

Requires Python 3 and Git. Run from the repository root.

**Windows (PowerShell)**

```powershell
python -m venv env
.\env\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

**macOS / Linux**

```bash
python3 -m venv env
source env/bin/activate
python -m pip install -r requirements.txt
```

Check it worked:

```bash
python -c "import google.cloud.storage, google.cloud.bigquery, faker; print('ok')"
```

The `env/` folder is ignored by Git. Rebuild it from `requirements.txt` instead of committing it.

## Stack

Python, Faker, Cloud Storage, BigQuery, Dataform, pytest, GitHub Actions