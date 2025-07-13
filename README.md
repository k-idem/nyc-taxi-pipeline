# nyc-taxi-pipeline

A compact, end-to-end batch pipeline:

* **Ingest** — download January-2023 Yellow Taxi data  
* **Land** — store Parquet in Google Cloud Storage  
* **Load** — stage into BigQuery (`yellow_2023_part`)  
* **Transform** — build `dim_*` and `fact_*` tables with dbt  
* **Orchestrate** — one Kestra flow triggers every step  

---

## Architecture

![diagram](diagrams/architecture.png)

---

## Quick start

```bash
# spin up Kestra
cd ~/projects/data-engineering-zoomcamp/02-workflow-orchestration
docker compose up -d               # -d = detached background run

# Kestra UI → http://localhost:8080
# 1. Flows ▸ Import  →  flows/nyc_taxi_capstone.yaml
# 2. Settings ▸ Secrets → add:
#    GCP_CREDS, GCP_PROJECT_ID, GCP_BUCKET_NAME, GCP_DATASET
# 3. Click “Run” and watch the DAG turn green
```

---

## Proof

| Stage          | Screenshot                              |
|----------------|-----------------------------------------|
| Kestra DAG     | ![](images/dag.png)                     |
| BigQuery table | ![](images/bq_table.png)                |
| dbt lineage    | ![](images/lineage.png)                 |

---

## Clean-up

```bash
docker compose down                    # stop Kestra stack
gcloud compute instances list \        # verify no stray VMs
  --filter="status:RUNNING"
```
>>>>>>> cf7aa45 (Scaffold project: folders, flow, README stub)
