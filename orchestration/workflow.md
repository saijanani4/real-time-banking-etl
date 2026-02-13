%md
# Runbook / Troubleshooting

## Common Issues

### 1) No new data ingested but job succeeds
**Cause:** No new files arrived in the raw `incoming/` path since last run.
**Fix:** Run the transaction generator to create new batches, then rerun the pipeline.

---

### 2) Job cluster fails to start (GCP quota exceeded)
**Example:** `SSD_TOTAL_GB quota exceeded`
**Cause:** Cloud quota limitations in the GCP region.
**Fix options:**
- Reduce disk size for the job cluster
- Use an existing all-purpose cluster temporarily
- Request quota increase in GCP Quotas for the region

---

### 3) Notebook path not found (after refactor)
**Cause:** Workflow task points to old notebook path or `%run` references are absolute.
**Fix:** Use repo-relative paths for config imports:
`%run ../config/00_config_and_helpers`

---

### 4) Power BI connection errors
**Cause:** Connector/driver mismatch.
**Fix:** Install the latest 64-bit Power BI Desktop (MSI), then reconnect using Databricks SQL Warehouse hostname + HTTP Path + PAT.
