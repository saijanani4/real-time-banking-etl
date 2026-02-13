%md
# Databricks Workflows (Dev & Prod)

## Overview
This project uses Databricks Workflows to orchestrate a Medallion pipeline:
Bronze (streaming ingest) → Silver (clean/enrich) → Gold (business KPIs).

Two environments are supported:
- **dev**: manual runs for iteration/testing
- **prod**: scheduled run (daily) using a job cluster

---

## Workflow: Finance_ETL_Pipeline_dev
**Purpose:** fast iteration + debugging

**Tasks (in order):**
1. `Data_Ingestion` → `src/ingestion/02_bronze_ingestion`
2. `Data_Transformation` → `src/transformation/03_silver_transformation`
3. `Data_Loading` → `src/transformation/04_gold_aggregations`

**Parameters**
- `env = dev`

**Compute**
- Job cluster (isolated runs)

**Screenshot**
- `images/job_dev_graph.png`

---

## Workflow: Finance_ETL_Pipeline_prod
**Purpose:** scheduled production refresh for reporting

**Tasks (in order):**
1. `Data_Ingestion` → `src/ingestion/02_bronze_ingestion`
2. `Data_Transformation` → `src/transformation/03_silver_transformation`
3. `Data_Loading` → `src/transformation/04_gold_aggregations`

**Parameters**
- `env = prod`

**Schedule**
- Daily at **07:00 AM** (local time)

**Compute**
- Job cluster (isolated runs)

**Screenshot**
- `images/job_prod_schedule.png`

---

## Notes
- Streaming ingestion uses checkpointing to avoid duplicate processing.
- Gold tables are overwritten per run to represent the latest curated KPIs.
