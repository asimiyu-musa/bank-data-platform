# Bank Data Platform

## Goal
Build a production-ready, multi-environment (Dev / Prod) data pipeline on AWS for banking data.  
The platform follows the Medallion architecture (Bronze → Silver → Gold) and is fully managed with Terraform + GitHub Actions.

## Architecture Summary
- **Ingestion**: S3 + EventBridge / Kinesis
- **Processing**: AWS Glue + Step Functions
- **Storage**: S3 Data Lake (Bronze / Silver / Gold)
- **Orchestration**: Step Functions + EventBridge
- **Analytics**: Athena / Redshift Serverless
- **Infrastructure**: Terraform (multi-account / multi-env)

> Detailed diagram available in [`docs/architecture.md`](docs/architecture.md)

## Naming Convention
All resources follow this pattern:


Examples:
- `bank-dev-bronze-raw-transactions`
- `bank-prod-gold-customer-metrics`
- `bank-dev-glue-job-transactions-cleaner`

Bucket suffix (optional uniqueness): `-asimiyu` or your initials.

## Promotion Flow
1. Develop & test in **Dev** environment
2. Create a Pull Request
3. GitHub Actions runs `terraform plan` on Dev
4. After approval → merge to `main`
5. Manual approval required for **Prod** deployment
6. GitHub Actions applies changes to Prod