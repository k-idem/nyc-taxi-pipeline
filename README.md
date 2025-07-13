# NYC Taxi Pipeline 🚕✨

End-to-end batch pipeline built for the Data Engineering Zoomcamp capstone.

| Stage | Tool | What happens |
|-------|------|--------------|
| Ingest | Kestra HTTP task | Download January-2023 Yellow Taxi parquet |
| Land  | Google Cloud Storage | File saved to **dtc-data-lake-* $PROJECT_ID*** |
| Load  | BigQuery | External → partitioned table `yellow_2023_part` |
| Transform | dbt | Build `dim_` & `fact_` tables |
| Orchestrate | Kestra | Single DAG runs every step |
| IaC | Terraform (separate repo) | Demo S3 remote-state |
