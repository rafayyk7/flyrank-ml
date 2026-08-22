# 📢 Tell the Story: 5-Minute Demo Outline & Shareable Cuts

**Track:** Machine Learning (Week 8 Submit Phase)  
**Code:** ML-12  
**File Path:** `work/story_and_showcase.md`  
**Deployed Paper:** [https://rafayyk7.github.io/flyrank-ml/paper.html](https://rafayyk7.github.io/flyrank-ml/paper.html)  

---

## 🎙️ Part 1: 5-Minute Showcase Demo Outline

### Minute 1: The Problem & The Question (0:00 - 1:00)
* **Hook:** Enterprise websites lose organic search traffic quietly long before rankings fall off page 1.
* **The Industry Flaw:** Most content teams rely on crude heuristics (e.g., *"flag any page untouched for 180 days"*), which burns finite editorial budgets on low-value pages while missing high-risk URLs.
* **Core Question:** Can a gradient-boosted ML model out-predict heuristic baselines on forward 30-day traffic decay across multi-domain enterprise data?

### Minute 2: The Method & Validation Architecture (1:00 - 2:00)
* **Data Processing:** Refactored row-by-row Pandas loops into zero-copy vectorized DuckDB SQL views, slashing latency from 84.3s to 1.4s.
* **Leakage Guard:** Standard random K-Fold splits leak domain styles and authority. We enforced strict **5-Fold GroupKFold validation** grouped strictly by `domain_id`, isolating unseen domains into validation holdouts.

### Minute 3: One Chart — The Action Archetype Distribution (2:00 - 3:00)
* **Visual Focus:** `work/figures/action_archetypes.png`
* **Interpretation:** Rather than dumping a raw probability score, predictions are segmented into 4 actionable operational queues: *High-Value Decay (23.8%)*, *SERP Suppression (14.3%)*, *Zombie Content (8.3%)*, and *Stable Baseline (53.6%)*.

### Minute 4: One Honest Result (3:00 - 4:00)
* **The Metric:** `HistGradientBoosting` achieved an out-of-fold **ROC-AUC of 0.8215** (+20.1% lift over the 0.6842 heuristic baseline).
* **Defensible Framing:** We observed a strong directional correlation between staleness, position stability, and decay risk; we do not claim staleness is the sole causal driver due to external search engine algorithmic shifts.

### Minute 5: One Recommendation & Playbook (4:00 - 5:00)
* **The Action:** Focus editorial overhaul hours exclusively on *High-Value Decay* pages (`decay_probability >= 0.65` and `impressions_90d >= 2500`).
* **Governance Guardrail:** Human editor sign-off is mandatory before republishing; automated CMS text deletion or unreviewed LLM writes are strictly forbidden.

---

## 📱 Part 2: Shareable Cuts

### Cut 1: Technical Social Post (LinkedIn / X)

> Most ML models for search look impressive in a notebook because they quietly leak data across client domains.
> 
> When predicting organic search traffic decay across multi-domain interaction datasets, random K-Fold splits produce artificially high accuracy by memorizing domain-level authority signals.
> 
> In my latest research artifact at FlyRank, I built a leak-free gradient boosted decision tree pipeline:
> 
> 🔹 **Vectorized Ingestion:** Zero-copy DuckDB SQL queries over 90-day lookback windows (84.3s ➔ 1.4s compute time).  
> 🔹 **Leak-Free Validation:** Strict 5-Fold GroupKFold splitting by domain_id to evaluate true out-of-domain generalization.  
> 🔹 **Measured Impact:** Achieved 0.8215 out-of-fold ROC-AUC (a +20% lift over standard industry heuristic rules).  
> 🔹 **Action Playbook:** Mapped predictions into 4 human-in-the-loop editorial archetypes to preserve high-risk organic traffic.
> 
> 📄 Read the full deployed research paper and inspect the reproducibility receipts here:  
> https://rafayyk7.github.io/flyrank-ml/paper.html
> 
> #MachineLearning #DataSystems #SEO #DuckDB #Python #DataScience

---

### Cut 2: 3-Sentence Employer Summary (For CV, Portfolio, or Interview Intro)

1. **What I Built:** I engineered an end-to-end, leak-free machine learning scoring pipeline and automated Content Action Playbook that predicts 30-day organic search visibility decay.
2. **On What Data:** Evaluated on multi-domain search interaction datasets using zero-copy DuckDB vectorized views over 90-day historical lookback windows and strict 5-Fold GroupKFold domain validation.
3. **What It Showed:** The gradient boosted model achieved an out-of-fold ROC-AUC of 0.8215 (a 20.1% lift over heuristic rule baselines) while reducing batch feature compute latency from 84.3s down to 1.4s.
