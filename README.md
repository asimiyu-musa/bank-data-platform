# bank-data-platform

## Goal
A production-style data platform on AWS for a synthetic retail banking
dataset. Built to practise what separates a practice pipeline from a
production one: reliability, data quality, security, observability and
CI/CD with separate dev and prod environments.

## Architecture
Data flows through these layers:
- Generator: synthetic customers, accounts and transactions
- Bronze (S3): raw, immutable files
- Silver (Glue PySpark): cleaned, deduplicated, PII masked, bad rows quarantined
- Gold (Glue PySpark): daily balances and spend aggregates
- Redshift: staging, merge and serving
- Airflow: orchestration, retries and backfills

Cross-cutting: data quality gates, CloudWatch and SNS alerts,
IAM/KMS/Lake Formation security, Terraform and GitHub Actions.

Diagram: docs/[your-diagram-file]

## Naming convention
Pattern: bank-{env}-{layer}
- Environments: dev, prod
- Layers: bronze, silver, gold, quarantine
- Bucket suffix: [your suffix], for global uniqueness
- Example: bank-dev-bronze-[suffix]
- Every resource is tagged project = bank-data-platform

## Promotion flow
1. Create a feature branch
2. Open a pull request (CI runs checks)
3. Merge to main, which deploys to dev automatically
4. Verify in dev
5. Approve, and the same code deploys to prod

## Status
[Phase 1: foundations in progress]