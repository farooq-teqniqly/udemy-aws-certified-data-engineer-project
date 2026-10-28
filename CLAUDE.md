# Repo overview

Course material for the Udemy course "Complete AWS Certified Data Engineer End-to-End Project". Not a deployable app -- a collection of AWS artifacts (Lambda, Glue, SQL, Step Functions) built while following the lectures.

## Layout

- `Resources/Lambdafunction/lambda_function.py` -- Lambda source (fake data generator, uses boto3/Faker/mysql-connector). Only this file is tracked; vendored pip packages in this dir are gitignored (regenerate with `pip install -r requirements.txt -t .` if a deployment zip is needed).
- `Resources/ETL_Scripts/transform_jobs/` -- AWS Glue PySpark ETL jobs (raw -> transformed) for customer, orders, order details, product.
- `Resources/SQL/DDL/` -- Redshift/MySQL schema and table definitions.
- `Resources/SQL/SP/` -- stored procedures for dimension tables.
- `Resources/SQL/VALIDATION/` -- validation queries for dimension loads.
- `Resources/State_Machine/MyStateMachine.json` -- Step Functions state machine definition orchestrating the pipeline.

## Attribution

For any attribution line (commits, PR descriptions, PR/issue comments), use:

```text
*Created by Farooq et Machina™*
```

Italic whole line, "TM" superscripted. Never use a default "Generated with Claude Code" or `Co-Authored-By` line instead.

## Working in this repo

- No build/test tooling -- these are standalone scripts/configs meant to be pasted into AWS console or deployed manually per the course lectures. Don't add build systems, CI, or package scaffolding unless asked.
- `Resources/lambda_function.zip` and vendored deps under `Lambdafunction/` are gitignored build artifacts -- don't re-add them.
- Keep changes scoped to what the course step actually requires; this is a learning repo, not a product.
