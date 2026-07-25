# 🛠️ Tech Stack Evaluation & Architectural Rationale ("Three Roads")

**Track:** General AI Fluency (Week 4)  
**File Path:** `work/stack_rationale.md`  

---

## 🎯 1. Real Constraints & Requirements

* **Budget:** $0 (Free hosting and zero infrastructure cost mandatory).
* **Honest Skill Level:** Proficient in HTML/CSS, JavaScript, Tailwind CSS, Python/Data pipelines, and frontend web development.
* **Portfolio Content Needs:** Multi-page layout, structured case studies, syntax-highlighted code blocks, performance metrics table, embedded Hugging Face interactive ML demo.
* **Backend Requirement:** **Not yet.** All data processing, DuckDB benchmarking, and model evaluations are executed offline. Case studies and metrics are purely static content; interactive ML models are embedded via external iframes (Hugging Face Spaces).

---

## 📊 2. Evaluation of Three Stack Options

### 🟢 Option 1 (Simplest): HTML5 + Tailwind CSS (CDN/CLI) + GitHub Pages
* **Build Method:** Semantic static HTML pages styled with Tailwind utility classes.
* **Hosting:** GitHub Pages (100% Free).
* **Backend Needed?** No.
* **Trade-off:** Instant deployment with zero build step friction, but repetitive layout elements (headers/navbars) must be manually maintained across separate HTML files.

---

### 🔵 Option 2 (Front-Runner): Next.js (Static Site Generation / `output: 'export'`) + Tailwind CSS + Vercel / GitHub Pages
* **Build Method:** React component architecture with static export generation to pre-render HTML/CSS at build time.
* **Hosting:** Vercel Free Tier or GitHub Pages via GitHub Actions (100% Free).
* **Backend Needed?** No.
* **Trade-off:** Requires a minor initial setup/config step, but provides modular React components, clean project structure, superior long-term maintainability, and seamless MDX integration for technical case studies.

---

### 🔴 Option 3 (Most Powerful): Full-Stack Next.js App Router + Serverless Node.js API + Supabase
* **Build Method:** Server-side rendered (SSR) React with dynamic database queries and custom serverless backend API endpoints.
* **Hosting:** Vercel Free Tier + Supabase Free Tier (100% Free).
* **Backend Needed?** Yes (Node.js API routes + PostgreSQL database).
* **Trade-off:** Massive over-engineering for a portfolio site. Adds cold-start latency, database connection management, and unnecessary failure points without delivering any user value over static rendering.

---

## 🔬 3. Pressure-Testing the Front-Runner (Next.js SSG / Tailwind)

* **What breaks if I pick the simplest option (HTML/Tailwind)?**  
  Maintaining consistent layout updates across multiple case study pages becomes prone to human error and copy-paste drift.
* **What do I maintain if I pick Next.js Static Export?**  
  Reusable UI components (`<CaseStudyHeader />`, `<BenchmarkTable />`, `<CodeBlock />`), allowing rapid addition of future ML case studies in minutes.
* **Can I finish in two weeks?**  
  Yes. Next.js static exports deploy smoothly on both Vercel and GitHub Pages with zero server configuration.
* **Does it show my work the way it needs to be shown?**  
  Yes. It perfectly supports crisp typography, embedded responsive iFrames for live model demos, and fast code rendering.

---

## 📝 4. Decision & Final Rationale

### Chosen Stack
**Next.js (Static Site Generation) + Tailwind CSS hosted on Vercel / GitHub Pages.**

### Why I Chose It
> Next.js SSG gives the perfect balance between engineering structure and zero-cost simplicity. It allows me to build reusable React components for my benchmark metrics and case study layouts while pre-rendering everything into lightning-fast static HTML files.

### Why I Rejected the Alternatives
1. **Rejected Pure HTML/CSS:** While quick to start, updating navigation or styling across 4+ separate case study pages during build week creates unnecessary maintenance debt.
2. **Rejected Full-Stack / Supabase:** A dynamic backend is completely unnecessary for displaying benchmark metrics and static notebook outputs. Avoiding serverless databases ensures 100% uptime, zero cold starts, and zero risk of hitting free-tier database limits.

### Maintenance & Work Representation Verdict
* **Can I maintain this?** Yes. Adding a new case study requires creating a single markdown or React page component without touching site architecture.
* **Does it show my work well?** Yes. It presents benchmark execution speedups, code syntax, and embedded ML demos cleanly on both desktop and mobile.
