# 🤖 Capstone Agent Design Specification: Machine Learning Research & Code Review Scout

**Track:** General AI Fluency (Week 5 Build Phase)  
**Code:** FL-06  
**Target Build Scope:** ~8–10 Build Hours  
**File Path:** `work/agent_design_spec.md`  

---

## 🎯 1. Job to Be Done (JTBD) & User Profile

* **Core Job:** Automatically ingest machine learning research papers, technical blog posts, or local repository PRs/notebooks; summarize architectural takeaways; audit for data/target leakage; and draft benchmark experiments matching our repository standards.
* **Primary User:** Machine Learning Engineer & Engineering Sciences Researcher.
* **Usage Frequency:** 3–5 times per week during sprint research, experiment tracking, and codebase audits.

---

## 🛠️ 2. Tools, Data Sources & Access Plan

| Tool / Data Source | Type | Access Mechanism & Auth Plan | Purpose |
| :--- | :--- | :--- | :--- |
| **Local File System (MCP)** | Tool | Local MCP Filesystem Server (`read_file`, `write_file`) | Reads local notebooks (`work/notebooks/*.ipynb`) and benchmark metrics. |
| **ArXiv & Web Search API** | Tool | DuckDuckGo Search API / ArXiv Public REST API (Free) | Gathers primary paper abstracts, citation links, and methodology notes. |
| **DuckDB / CSV Query Tool** | Tool | In-process DuckDB Python Connector | Queries local warehouse slices (`gsc_url_daily`) to verify signal distributions. |
| **Git Automation Bridge** | Tool | Local Git CLI execution (Subprocess wrapper) | Reads git status, inspects active diffs, and prepares commit messages. |

---

## ⚙️ 3. Draft Agent Instructions (System Prompt)

```text
You are the ML Research & Code Review Scout. Your job is to analyze ML literature, verify data pipelines, and audit code for methodological flaws.

Execution Guidelines:
1. Grounding First: Base all technical explanations on cited reference files or live tool outputs. Never invent benchmark speedups or library syntax.
2. Leakage Guard: When reviewing data split code, verify that grouping constraints (e.g., domain_id or time-based splits) prevent future-window or target leakage.
3. Restraint & Scaffolding: Provide structured outputs (Tables, Markdown lists, JSON receipts). Keep high-level summaries under 200 words.
4. Human Approval: Never commit code, delete files, or send external API updates without explicit confirmation.
