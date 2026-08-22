# 🤖 ML Research & Code Review Scout (Autonomous Agent)

**Author:** Abdul Rafay Khan  
**Track:** General AI Fluency (FlyRank)  

## 🎯 What It Does & For Whom
This project features an autonomous Python agent designed for Machine Learning Engineers and Code Reviewers. The agent's core job is to autonomously inspect local ML Jupyter notebooks and JSON metric receipts, audit the validation splits for target leakage (specifically verifying `GroupKFold` usage), compute the ROC-AUC performance lift against baselines, and write an immutable Markdown audit report to disk.

## 🏗️ Architecture Sketch

[Human Trigger] ──> [ResearchScoutAgent]
                           │
                           ├── 🔧 Tool 1: `read_file()`
                           │      └── Probes local .ipynb AST for GroupKFold leakage guards.
                           │
                           ├── 🔧 Tool 2: `audit_metrics()`
                           │      └── Parses .json receipts to verify ROC-AUC lift.
                           │
                           └── 🔧 Tool 3: `write_report()`
                                  └── Synthesizes findings into `agent_audit_report.md`.

## 🚀 Setup & Usage Instructions
A stranger can reproduce this agent environment locally. It requires zero API keys and relies on standard Python libraries.

**1. Clone the repository:**
git clone https://github.com/rafayyk7/flyrank-ml.git
cd flyrank-ml

**2. Run the Autonomous Agent:**
Execute the agent script from your terminal:
python scripts/research_scout_agent.py

**3. Usage Example / Output:**
The agent will output live tool-call logs to the terminal:
🔧 [Tool Call]: Executing audit_metrics...
🔧 [Tool Call]: Executing read_file...
✅ [Agent Completed]: SUCCESS: Written to work/outputs/agent_audit_report.md

## 📊 v2 Evaluation Results
* **Execution Speed:** The agent executes its full end-to-end tool loop in ~1.14 seconds.
* **Autonomy:** Achieves a 100% success rate completing its core job end-to-end without mid-run human hand-editing or intervention.

## ⚠️ Known Limitations & Guardrails
1. **Offline Scope (No Web Search):** The original spec included a live ArXiv web scraper. This was intentionally scoped out of the MVP to act as a strict guardrail, keeping execution deterministic, offline-capable, and immune to third-party API timeouts.
2. **Hardcoded File Paths:** Currently, the agent assumes the target files are always located at `work/notebooks/w05_model.ipynb` and `work/outputs/w05_model_metrics.json`. It cannot currently crawl a dynamic directory tree to find varying notebook names.

## 🤖 AI Transparency
*I built this agent with an AI acting as a pair-programming partner. AI was utilized to draft the initial Python class structure and help format the tool schemas. I manually verified the file-reading logic and the ROC-AUC validation checks to ensure the agent was strictly evaluating the data without hallucinating results.*
