# 🏛️ Consistency, Not Talent: Design System & Framing Rationale

**Track:** General AI Fluency (Week 3 Foundations)  
**File Path:** `work/consistency_and_framing.md`  
**Reference Specification:** [FlyRank Week 3 Curriculum](https://aifluency.flyrank.ai/week-03.html)

---

## 🎯 1. The Intentionality Choices (Consistency Over Talent)

Amateur portfolios fail due to visual noise: mismatched typefaces, arbitrary gradients, and uneven layout spacing. Professional intentionality requires only a few strict constraints:

### Typography System
* **Heading Font:** [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) (Weights: 600 SemiBold, 700 Bold) — clean, structured, and modern for clear hierarchy.
* **Body Font:** [Inter](https://fonts.google.com/specimen/Inter) (Weights: 400 Regular, 500 Medium) — highly legible across high-density data tables and benchmark logs.

### Locked Color Palette

| Role | Color Name | Hex Code | Purpose |
| :--- | :--- | :--- | :--- |
| **Background** | Dark Slate | `#0F172A` | Deep, low-contrast backdrop that reduces eye strain. |
| **Surface / Light Mode** | Slate Light | `#F8FAFC` | High-contrast neutral for readable text containers. |
| **Primary Text** | Off-White | `#F1F5F9` | Crisp contrast without harsh 100% white glare. |
| **Accent** | Cobalt Blue | `#2563EB` | Single focal color for CTAs, active states, and metric callouts. |
| **Muted Text / Border** | Slate Muted | `#64748B` | Subtle boundaries that don't compete with content. |

---

## 🖼️ 2. The Core Rule: Frame the Work, Never Upstage It

An engineering portfolio is not an art gallery; it is a repository of technical proof. 

* **The Canvas:** Real execution metrics (e.g., 84.3s $\rightarrow$ 1.4s DuckDB refactoring, $n=5,000$ warehouse row checks, leak-free feature validation).
* **The Frame:** A quiet, minimalist container (`#0F172A` background, 2-font system, single `#2563EB` accent). 
* **Design Boundary:** No distracting parallax animations, no neon gradients, and no generic 3D illustrations. The technical metrics and code architecture remain the loudest elements on every page.

---

## ⚖️ 3. Image Discernment: Authentic Proof vs. Synthetic Generation

AI image generation is fast, making **editorial restraint** the primary skill.

```text
               ┌──────────────────────────────────────────────┐
               │         PORTFOLIO VISUAL SEPARATION          │
               └──────────────────────┬───────────────────────┘
                                      │
         ┌────────────────────────────┴────────────────────────────┐
         ▼                                                         ▼
┌───────────────────────────────┐         ┌────────────────────────────────┐
│   AUTHENTIC PROOF (Real)      │         │   CONNECTIVE TISSUE (AI)       │
├───────────────────────────────┤         ├────────────────────────────────┤
│ • Personal Headshot Photo     │         │ • Flat Geometric Backgrounds   │
│ • VS Code Terminal Outputs    │         │ • Minimalist Vector Tech Icons │
│ • Colab Execution Logs        │         │ • Strict Palette Enforced      │
│ • DuckDB Benchmark Traces     │         │ • Zero Fake Synthesized UI     │
└───────────────────────────────┘         └────────────────────────────────┘
