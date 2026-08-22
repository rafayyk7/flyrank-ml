# 🤖 ML Research & Code Review Scout (Autonomous Agent)

**Author:** Abdul Rafay Khan  
**Track:** General AI Fluency (FlyRank)  

## 🎯 What It Does & For Whom
This project features an autonomous Python agent designed for Machine Learning Engineers and Code Reviewers. The agent's core job is to autonomously inspect local ML Jupyter notebooks and JSON metric receipts, audit the validation splits for target leakage (specifically verifying `GroupKFold` usage), compute the ROC-AUC performance lift against baselines, and write an immutable Markdown audit report to disk.

## 🏗️ Architecture Sketch

```text
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
🚀 Setup & Usage Instructions
A stranger can reproduce this agent environment locally. It requires zero API keys and relies on standard Python libraries.

1. Clone the repository:
git clone [https://github.com/rafayyk7/flyrank-ml.git](https://github.com/rafayyk7/flyrank-ml.git)
cd flyrank-ml
2. Run the Autonomous Agent:

Execute the agent script from your terminal:
python scripts/research_scout_agent.py

3. Usage Example / Output:
The agent will output live tool-call logs to the terminal:
🔧 [Tool Call]: Executing audit_metrics...
🔧 [Tool Call]: Executing read_file...
✅ [Agent Completed]: SUCCESS: Written to work/outputs/agent_audit_report.md

You can then open work/outputs/agent_audit_report.md to view the agent's final synthesized verdict.

2. Run the Autonomous Agent:
Execute the agent script from your terminal:

Bash
python scripts/research_scout_agent.py
3. Usage Example / Output:
The agent will output live tool-call logs to the terminal:
🔧 [Tool Call]: Executing audit_metrics...
🔧 [Tool Call]: Executing read_file...
✅ [Agent Completed]: SUCCESS: Written to work/outputs/agent_audit_report.md

You can then open work/outputs/agent_audit_report.md to view the agent's final synthesized verdict.
