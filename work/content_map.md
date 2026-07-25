# 🗺️ Portfolio Content Map & Through-Line Architecture

**Track:** General AI Fluency (Week 3)  
**File Path:** `work/content_map.md`  

---

## 🎯 1. The One-Line Claim

> **"I build production-ready machine learning pipelines and high-throughput data architectures that convert raw interaction signals into sub-second, measurable business impact."**

---

## 📐 2. Site Architecture & Page-by-Page Content Map

### 📄 Page 1: Home / Portfolio Hub
* **Order of Sections:**
  1. **Hero Section:** One-Line Claim + Headshot + Direct links to GitHub & Resume.
  2. **Featured Case Study (Lead with Strongest Work):** Recommendation Scoring Engine Refactor (CollabIn).
  3. **Secondary Case Study:** Content Decay Prediction Engine (FlyRank Search Intelligence).
  4. **Engineering Stack & Technical Identity:** Interactive matrix of core tools (Python, DuckDB, Pandas, Scikit-Learn, Next.js).
* **Lead Case:** CollabIn High-Throughput Recommendation Refactor (84.3s to 1.4s optimization over 1.8 GB dataset).
* **Call to Action (CTA):** `"Explore Full Case Studies"` $\rightarrow$ Links directly to the Lead Case Study page.

---

### 📄 Page 2: Case Study 1 — CollabIn High-Throughput Recommendation Engine (Strongest Work)
* **Order of Sections:**
  1. **Impact Summary Bar:** 1.8 GB dataset / 4.2M rows processed in **1.4s** (down from 84.3s) with 0 RAM crashes.
  2. **The Bottleneck:** Legacy Pandas `.apply()` row processing choking local memory.
  3. **Architectural Solution:** Zero-copy DuckDB streaming views & vectorized SIMD SQL scoring.
  4. **Code & Benchmark Proof:** Embedded runnable script snippet and `psutil` RAM usage logs.
* **Call to Action (CTA):** `"View Next Case Study: Search Intelligence Pipeline"` $\rightarrow$ Guides the visitor logically to Case Study 2.

---

### 📄 Page 3: Case Study 2 — FlyRank Search Intelligence & Content Decay Model
* **Order of Sections:**
  1. **Problem Framing:** Predicting 30-day organic impression decay across 32 client domains.
  2. **Data Contract & Leakage Prevention:** `GroupKFold` cross-validation grouped strictly by `domain_id`.
  3. **Metric Optimization:** Precision@50 evaluation aligned with operational rewrite budgets.
  4. **Model Performance & Confusion Matrix:** Holdout precision scores and feature importance charts.
* **Call to Action (CTA):** `"Inspect Code Repository on GitHub"` $\rightarrow$ Sends visitor to inspect raw engineering execution.

---

### 📄 Page 4: About & Engineering Workflow
* **Order of Sections:**
  1. **Background & Mindset:** CS & Engineering focus on scalable data pipelines and AI fluency.
  2. **AI Tooling & Workflow Audit:** How prompt engineering and AI assistants accelerate local iteration speed.
  3. **Contact & Next Steps:** Professional connections and availability.
* **Primary Call to Action (Laddering to Week 1 Goal):** `"Schedule a Technical Sync"` / `"Connect on LinkedIn"` $\rightarrow$ Converts portfolio views into direct recruiter outreach.

---

## 📋 3. Proof Still Needed to Gather ("Gather List")

| Project | Needed Asset | Status / Plan | Blocked? |
| :--- | :--- | :--- | :--- |
| **CollabIn Internship** | Final benchmark memory trace graph (`psutil` RAM logs) | To be exported from local test run | 🟢 No |
| **CollabIn Internship** | Internship task confirmation / recommendation note | Requesting brief confirmation snippet | 🟢 No |
| **FlyRank Capstone** | Live interactive demo link (Hugging Face Spaces) | To be deployed in modeling phase | 🟢 No |
| **FlyRank Capstone** | Cleaned baseline performance charts | Will capture output from notebook 04 | 🟢 No |
| **Portfolio Infrastructure** | Cleaned GitHub repository READMEs | In progress across `flyrank-ml` | 🟢 No |
