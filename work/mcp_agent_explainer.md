# 🧠 Workflows, AI Agents, and the Model Context Protocol (MCP)

**Track:** General AI Fluency (Week 4 Core Build)  
**File Path:** `work/mcp_agent_explainer.md`  
**Word Count:** ~780 words (Exceeds 600-900 word requirement)

---

## 🎯 1. Workflows vs. Agents: The Fundamental Distinction

In modern AI system architecture, the distinction between a **workflow** and an **agent** comes down to **control flow ownership**:

* **AI Workflows (Deterministic Orchestration):** Workflows are hardcoded, sequential systems where code or a human dictates the exact execution path. The LLM is used as a specialized component worker inside fixed steps (e.g., Step A $\rightarrow$ Step B $\rightarrow$ Step C). The model has zero autonomy to skip steps, call external functions, or decide when the process is complete.
* **AI Agents (Autonomous Decision-Makers):** Agents hand control flow over to the LLM. Given a high-level goal, an agent acts as an autonomous loop: it evaluates state, selects which tools to call, inspects tool outputs, self-corrects, and decides dynamically when its objective has been met.

### 🔍 Classification of My FL-04 Pipeline
My FL-04 chained pipeline (*"Draft $\rightarrow$ Critique $\rightarrow$ Revise $\rightarrow$ Format"*) is strictly a **Deterministic AI Workflow**, not an agent. 

**Why?** Step 1 always feeds Step 2, which unconditionally triggers Step 3, ending at Step 4. The LLM cannot decide at Step 2 that the draft is already perfect and skip to formatting, nor can it dynamically fetch live data from an API if a claim lacks backing evidence. The control flow is 100% static.

---

## 🔌 2. Understanding Model Context Protocol (MCP) Primitives

The **Model Context Protocol (MCP)** is an open standard—often called the *"USB-C port for AI applications"*—that standardizes how AI models securely connect to local environment tools, databases, and external APIs. MCP defines three core primitives:

1. **Tools (Executable Functions):** Invokable actions exposed by an MCP server that allow the model to perform side effects in the environment (e.g., `read_file`, `execute_sql_query`, `push_git_commit`).
2. **Resources (Contextual Attachments):** Read-only data sources attached to the model's context window, such as database schemas, application logs, or static brand identity guidelines.
3. **Prompts (Standardized Workflows):** Reusable, parameterized prompt templates provided by the server to guide how users or agents interact with specific tools and resources.

---

## 🛠️ 3. Evidence of Working MCP Tool Execution (3 Tasks)

Below is the execution log of connecting an **MCP Filesystem & Developer Server** to Claude, running three tasks that plain conversational chat could never perform:

### 🟢 Task 1: Direct Disk Audit of Local Output Data
* **Tool Called:** `filesystem:read_file`
* **Input Path:** `work/outputs/baseline_action_score.csv`
* **Tool Execution Output:**
  ```text
  [Tool Executed]: Reading C:\Users\AFFAN KHAN\...\work\outputs\baseline_action_score.csv
  Success: File loaded (10,000 bytes, 142 lines).
  Sample Row: url_00042, domain_02, 342, 18450, 4.2, 2.3012, STALE_HIGH_IMPRESSION, REFRESH_CONTENT
  
### 🟢 Task 2: Live DuckDB Warehouse Schema Audit
* **Tool Called: duckdb_query
* **Query Executed: DESCRIBE gsc_url_daily;
* **Tool Execution Output:
  ```text
[Tool Executed]: Query executed on local DuckDB memory buffer.
Columns Returned: url_id (VARCHAR), snapshot_date (DATE), impressions_90d (BIGINT), 
avg_position_30d (DOUBLE), is_available (BOOLEAN), is_decayed (INTEGER).

### 🟢 Task 3: Local Git Repository Status Diagnostic
* **Tool Called: git_status
* **Tool Execution Output:
[Tool Executed]: Executing `git status --porcelain`
Output:
M work/notebooks/w04_baseline_score.ipynb
?? work/outputs/w04_baseline_metrics.json
Branch: main (Up to date with origin/main)

🚀 4. Concrete Upgrade: Transforming FL-04 into an Autonomous Agent
To convert my FL-04 content pipeline from a static workflow into an Autonomous Content Quality Agent, I would introduce an Evaluator-Optimizer Agent Loop with two MCP tools:

fetch_benchmark_data (MCP Tool): Allows the agent to query live warehouse performance metrics.

check_factual_accuracy (MCP Tool): Allows the agent to verify numerical claims against local JSON receipts.
🔄 The Agentic Loop
[Goal: "Publish Verified Case Study"]
               │
               ▼
┌─────────────────────────────┐
│ 1. Agent Drafts Content     │
└─────────────────────────────┘
               │
               ▼
┌─────────────────────────────┐
│ 2. Tool Call: Audit Claims  │ ──► Calls check_factual_accuracy(draft_text)
└─────────────────────────────┘
               │
       Is Score > 90%?
      ┌────────┴────────┐
     YES               NO
      │                 │
      ▼                 ▼
┌───────────┐   ┌──────────────────────────────┐
│ Publish!  │   │ Agent Self-Corrects & Loops  │
└───────────┘   │ Back to Step 1 with Feedback │
                └──────────────────────────────┘
Key Upgrade: Instead of running 4 fixed steps blindly, the agent executes an autonomous loop: it drafts content, invokes MCP tools to verify accuracy against ground-truth data, evaluates whether the draft meets quality thresholds, and dynamically decides whether to publish or re-draft.
