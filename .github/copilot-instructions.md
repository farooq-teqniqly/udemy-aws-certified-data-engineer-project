# Copilot instructions

This repository contains code written while following the Udemy course
"Complete AWS Certified Data Engineer End-to-End Project". It exists to learn
AWS data engineering techniques (Lambda, Glue ETL, Redshift/MySQL SQL, Step
Functions) -- it is not a production codebase and is not deployed anywhere.

## Review guidance

When reviewing pull requests or suggesting changes in this repo, keep feedback
light and relevant to whether the course exercise works:

- Do not flag hardcoded sample values, demo credentials/placeholders, or
  config meant for local/course use.
- Do not suggest adding error handling, logging, retries, input validation,
  or tests unless the course lecture at that point calls for it.
- Do not raise security-hardening, IAM least-privilege, secrets-management,
  or production-readiness concerns.
- Do not nitpick style, formatting, or general best practices that don't
  affect whether the exercise runs.
- Do not suggest performance, scalability, or cost-optimization changes.

Only raise an issue if there's an actual bug that would prevent the exercise
from working as the course intends.

## Layout

- `Resources/Lambdafunction/lambda_function.py` -- Lambda source for the fake
  data generator (boto3, Faker, mysql-connector).
- `Resources/ETL_Scripts/transform_jobs/` -- AWS Glue PySpark ETL jobs.
- `Resources/SQL/` -- DDL, stored procedures, and validation queries.
- `Resources/State_Machine/MyStateMachine.json` -- Step Functions definition.
