# 🛠️ Capstone Agent MVP Build Log (FL-07 / Checkpoint 1)

**Track:** General AI Fluency  
**Agent Name:** ML Research & Code Review Scout  
**File Path:** `work/agent_build_log.md`  

---

## 📋 1. Core Job & MVP Scope
The agent's single focused job is to inspect local machine learning notebooks and model receipts, audit split definitions for target leakage (`GroupKFold`), compute the performance lift against the baseline, and write an immutable audit report to disk.

---

## 🔄 2. Real Iteration & What Broke During the Build

### Iteration 1: The Raw JSON Notebook Parsing Bottleneck
* **What Broke:** In the first implementation, passing the entire raw `.ipynb` JSON file directly into context caused token buffer timeouts and slowed execution to over 45 seconds.
* **The Fix:** Shifted to targeted string search primitives inside `_tool_read_file` to directly probe AST code cells for `GroupKFold` split instances and domain groupings.

### Iteration 2: DuckDB File Lock Conflicts
* **What Broke:** Attempting to query `gsc_url_daily` while another process had an open DuckDB read lock triggered a `duckdb.IOException`.
* **The Fix:** Handled database connections using read-only in-memory copies and prioritized verified JSON receipts (`work/outputs/*.json`) for deterministic verification.

---

## ✂️ 3. Deviations & What Was Cut From the FL-06 Spec
* **Live ArXiv Web Scraper Cut for MVP:** The original spec called for querying live ArXiv API endpoints on every run. I scoped this out of Checkpoint 1 to keep total execution deterministic, offline-capable, and sub-2-seconds. Live search integration will be added in Checkpoint 2.

---

## 🔌 4. Live Tool Connections in Use
* **`read_file` (Filesystem Tool):** Directly reads `work/notebooks/w05_model.ipynb` from disk.
* **`audit_metrics` (Receipt Tool):** Parses JSON metrics and evaluates ROC-AUC delta against Week 4 baselines.
* **`write_report` (Disk Writer Tool):** Generates and commits `work/outputs/agent_audit_report.md`.

---

## 🎥 5. Verification Run Output
* **Run Execution:** `python scripts/research_scout_agent.py`
* **Result:** Zero mid-run human edits required. Executed in 1.14s. Report committed to `work/outputs/agent_audit_report.md`.
