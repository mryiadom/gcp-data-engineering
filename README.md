# GCP Data Engineering Portfolio

Batch data pipelines on Google Cloud, built from synthetic and public financial services data, alongside preparation for the Google Cloud Professional Data Engineer certification.

**Progress page:** [mryiadom.github.io/gcp-data-engineering](https://mryiadom.github.io/gcp-data-engineering/)

## About

I'm a Junior Data Engineer with an MEng in Mechanical Engineering, building towards data and analytics engineering roles in UK fintech, banking and capital markets. This repo is a 25-week plan at 5 to 10 hours a week, starting 19 October 2026. Each week ends in something committed here. Each project lives in its own folder, which links from this page once its first pull request is merged.

## Projects

| # | Project | What it shows | Weeks | Status |
|---|---------|---------------|-------|--------|
| A | **Card payments monitoring.** A card issuer's daily spending view and first line of fraud rules. | Python data generation, loads through Cloud Storage into partitioned BigQuery tables, Dataform star schema, window-function rules, assertions at every layer, pytest and CI | 1 to 9 | Planned |
| B | **FX trades and positions.** An FX desk's end-of-day positions and sterling revaluation P&L. | Public Bank of England rates kept as point-in-time history, trade amendments and cancellations, reconciliation and stale-rate checks, built in dbt | 14 to 19 | Planned |

All data is synthetic (generated with Faker) or public batch data. Nothing here touches live banking systems or real customer data.

A project counts as finished only when it has a README, an architecture diagram, a data model diagram, Dataform or dbt tests, sample outputs, and a "what I'd change in production" section.

## Stack, and why

| Tool | Role | Why it's here |
|------|------|---------------|
| SQL, Python | Core | Asked for in almost every junior data engineering and analytics engineering advert |
| Cloud Storage, BigQuery | Core | Landing zone and warehouse |
| Dataform | Core | SQL transformation and assertions, native to BigQuery |
| dbt | Added in week 12 | In UK BigQuery job adverts, dbt is named about five times as often as Dataform. Project A is rebuilt in dbt so both tools are covered |
| Airflow | Added in week 20 | Appears in around a quarter of UK BigQuery adverts. Runs locally in Docker to avoid managed-service costs |
| Pub/Sub, Dataflow | Exam only | Not asked for in junior adverts, so they're studied for the certification and not built into the projects |

Market evidence: IT Jobs Watch UK permanent adverts, six months to October 2026.

## Engineering standards

- **No secrets in git.** `.gitignore` covers key files, credentials and Terraform state, and the patterns are tested with `git check-ignore`. Cloud access uses Application Default Credentials, not downloaded keys.
- **Every change goes through a pull request.** `main` is protected, so there are no direct pushes.
- **Cost-aware tables.** Tables are partitioned and clustered, and queries are checked for bytes billed.
- **Idempotent loads.** Re-running a load must not duplicate data, and that is shown by running it twice.
- **Tested transforms.** Assertions or tests on keys, nulls and business rules. pytest and GitHub Actions run on every pull request from week 8.

## Cost control

Everything runs in one billing-enabled Google Cloud project in `europe-west2` (London), with a Cloud Billing budget alerting at 50%, 90% and 100%. Budgets alert but don't cap spend, so this is backed by small datasets, partition filters and query cost checks. Airflow and dbt Core run locally.

## Roadmap

| Phase | Weeks | Dates | Focus | Ends with |
|-------|-------|-------|-------|-----------|
| 0 | – | Oct 2026 | Baseline exam check, roadmap, project choice, repo safety | Done |
| 1 | 1 to 4 | 19 Oct to 15 Nov 2026 | Project A thin slice: scaffold, generator, loads, first Dataform models | Readiness check 1 |
| 2 | 5 to 9 | 16 Nov to 20 Dec 2026 | Project A complete: star schema, incremental loads, monitoring rules, tests and CI | Readiness check 2 |
| – | 10 to 11 | 21 Dec 2026 to 3 Jan 2027 | Holiday, exam reading only | |
| 3 | 12 to 19 | 4 Jan to 28 Feb 2027 | Project A in dbt, then Project B | Readiness check 3 |
| 4 | 20 to 25 | 1 Mar to 11 Apr 2027 | Airflow for both projects, timed mock exam, exam run-in | Final readiness check |

## Certification

Preparing for the **Google Cloud Professional Data Engineer** exam (guide v4.2). Every exam sub-section is mapped to a roadmap week. Readiness is scored per section at the end of each phase as Not started, Weak, Developing or Ready.

| Exam section | Weight |
|--------------|--------|
| 1. Designing data processing systems | ~22% |
| 2. Ingesting and processing the data | ~25% |
| 3. Storing the data | ~20% |
| 4. Preparing and using data for analysis | ~15% |
| 5. Maintaining and automating data workloads | ~18% |

## Repository layout

```
docs/          Progress page, served by GitHub Pages from main /docs
projects/      One folder per project (created in week 1)
```
