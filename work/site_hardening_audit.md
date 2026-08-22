# 🔨 "Break Your Own Site" Hardening & Diligence Audit

**Track:** General AI Fluency (Week 7 Submit Phase)  
**Live Tested Site:** `https://rafayyk7.github.io/flyrank-ml/`  
**File Path:** `work/site_hardening_audit.md`  

---

## 🧪 1. Edge-Case Stress Testing (How I Tried to Break It)

| Test Scenario | Input / Action Tested | Behavior Observed | Triage Category |
| :--- | :--- | :--- | :--- |
| **Empty Form Submission** | Clicked "Send Live Message" with all empty fields. | Browser prevented submission via HTML5 `required` flags. | ✅ Handled |
| **Garbage / Truncated Text** | Submitted `a` as name and `x` as message. | Backend rejected short messages without clear user-facing feedback. | **Fix-Now** |
| **Rapid Double-Clicking** | Clicked submit 3 times in 400ms. | Triggered duplicate POST dispatches and multiple API alerts. | **Fix-Now** |
| **Untested Browser Viewport** | Tested on Firefox Android (Landscape Mode, 812x375). | Top nav logo collided with links due to restricted vertical height. | **Fix-Now** |
| **Broken Link Audit** | Checked all repository, anchor, and mailto links. | All links resolve with 200 OK status; `_blank` tabs use `rel="noopener"`. | ✅ Handled |

---

## 🚦 2. Triage & Remediation Matrix

### 🟢 Fixed Now
* **Client-Side Form Safeguards:** Added `minlength="2"` on Name and `minlength="10"` on Message to prevent accidental empty/garbage dispatches.
* **Double-Submit Lockout:** Implemented a JavaScript event listener that disables the submit button immediately upon first click (`submitBtn.disabled = true; submitBtn.innerText = '⏳ Dispatching...'`).
* **Viewport Adaptability:** Adjusted navigation layout to prevent header collision on ultra-wide landscape mobile screens.

### 🟡 Known Limitations (Documented by Design)
* **Form Redirection Flow:** FormSubmit redirects through a third-party success page rather than an inline AJAX toast notification. *Rationale:* Kept as a pure zero-cost, static implementation without client-side API secret exposure.
* **Single Theme Locking:** Dark Slate (`#0F172A`) is hardcoded without a dynamic light mode toggle. *Rationale:* Preserves high-contrast readability across technical data tables without adding client-side state overhead.

---

## 🔍 3. Findability & SEO Metadata Check

* **Canonical Tag:** `<link rel="canonical" href="https://rafayyk7.github.io/flyrank-ml/" />`
* **Meta Description:** Formatted and indexed for search engines (152 characters).
* **Social Share Preview:** Open Graph (`og:title`, `og:description`, `og:url`) and Twitter Cards configured for rich rendering on LinkedIn and Discord/Slack.

---

## ⚡ 4. Google Lighthouse & Speed Check Audit

| Metric / Dimension | Measured Score | Standard |
| :--- | :--- | :--- |
| **Performance** | **99 / 100** | First Contentful Paint (FCP) < 0.6s |
| **Accessibility** | **100 / 100** | Contrast ratios > 14:1; 48px tap targets |
| **Best Practices** | **100 / 100** | HTTPS enforced; modern viewport tags |
| **SEO** | **100 / 100** | Crawlable links; valid document meta tags |
