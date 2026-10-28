# udemy-aws-certified-data-engineer-project

Code built while following the Udemy course
[Complete AWS Certified Data Engineer End-to-End Project](https://www.udemy.com/course/complete-aws-certified-data-engineer-end-to-end-project/learn/lecture/47739435#overview).

This is learning/demo code, not a production system. It implements an
end-to-end AWS data pipeline: fake UK sales data is generated into a MySQL
source, ingested to S3, transformed with Glue, loaded into Redshift, and
orchestrated with Step Functions.

## Pipeline

1. **Generate source data** -- a Lambda function (`Resources/Lambdafunction/lambda_function.py`)
   uses Faker to insert fake customer/order/product data into a MySQL
   database, pulling DB credentials from AWS Secrets Manager.
2. **Ingest to S3** -- MySQL tables are brought into S3 as raw data
   (via DMS/Glue crawler, per the course setup -- not scripted in this repo).
3. **Transform (raw -> curated)** -- AWS Glue PySpark jobs in
   `Resources/ETL_Scripts/transform_jobs/` clean and reshape each raw table:
   - `raw_customer_etl_job.py`
   - `raw_orders_etl_job.py`
   - `raw_orderdetails_etl_job.py`
   - `raw_product_etl_job.py`
4. **Load into Redshift** -- `Resources/SQL/DDL/` defines the source schema
   and target dimension/fact tables; `Resources/SQL/SP/` holds stored
   procedures (`customer_dim_sp.sql`, `products_dim_sp.sql`) that load
   dimension tables; `Resources/SQL/DDL/uk_sales_mart.sql` builds the
   auto-refreshing UK sales summary materialized view.
5. **Validate** -- `Resources/SQL/VALIDATION/dim_validation_sql.sql` checks
   the loaded dimension data.
6. **Orchestrate** -- `Resources/State_Machine/MyStateMachine.json` is a
   Step Functions definition that runs the Glue raw-transform jobs in
   parallel, then the load jobs, tying the pipeline together end to end.

## Layout

```text
Resources/
  Lambdafunction/lambda_function.py   # fake data generator Lambda (source only; deps gitignored)
  ETL_Scripts/transform_jobs/         # Glue PySpark ETL jobs (raw -> transformed)
  SQL/
    DDL/                              # MySQL source + Redshift schema/table definitions
    SP/                               # stored procedures for dimension table loads
    VALIDATION/                       # validation queries
  State_Machine/MyStateMachine.json   # Step Functions pipeline orchestration
```

## Notes

- `Resources/lambda_function.zip` and the vendored packages under
  `Lambdafunction/` are gitignored build artifacts; rebuild with
  `pip install -r requirements.txt -t Resources/Lambdafunction/` if you need
  a deployable zip.
- See `CLAUDE.md` for repo conventions (AI assistant guidance).
