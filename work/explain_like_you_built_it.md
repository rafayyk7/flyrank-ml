# 💡 Explain It Like You Built It: How GitHub Pages Ships a Live URL

**Track:** General AI Fluency (Week 5 Build+)  
**File Path:** `work/explain_like_you_built_it.md`  
**Chosen Feature:** The Automated GitHub Pages Deployment Pipeline (`index.html` ➔ Live URL)

---

## 🎯 The Part of the Build I Chose
When we created `index.html` and flipped the switch under **Settings ➔ Pages**, our code was suddenly reachable on a phone browser at `https://rafayyk7.github.io/flyrank-ml/`. I wanted to understand the exact mechanics of how a plain text file in a repository turns into a live, secure website without paying for a server or setting up domain routing manually.

---

## 🗣️ Plain-English Explanation (Teaching a Friend)

Imagine writing a flyer on your laptop. Normally, only people standing right in front of your screen can read it. 

To let anyone in the world read it, you need two things:
1. A public display board that never turns off (a web server).
2. An exact address so people know which street corner to walk to (a URL).

When we commit `index.html` to the `main` branch:
* **The Trigger:** GitHub acts like an automated printing press. The moment it detects a new save in the `main` branch, it triggers an internal worker (GitHub Actions).
* **The Convention:** The web expects an entry door named `index.html` by default. GitHub's server automatically looks for this exact filename at the root folder.
* **The CDN & HTTPS:** GitHub copies that file to high-speed distribution nodes (servers worldwide) and attaches a free security certificate (the padlock icon / HTTPS).
* **The Live URL:** It maps our account name and repo name (`rafayyk7` + `flyrank-ml`) into the public web domain `rafayyk7.github.io/flyrank-ml/`.

Whenever I edit a line of CSS or update the text and hit **Commit**, GitHub re-runs this entire pipeline in under 45 seconds, silently updating the flyer on the public board.

---

## 🔍 Why This Matters for My Architecture
Understanding this pipeline removed the "black box" fear of web hosting:
* **Zero Backend Overhead:** Because our portfolio case studies and metrics are pre-computed in Python/DuckDB, we don't need a live database server running 24/7. 
* **Immutable Version Control:** Every single live update is tied to a specific Git commit hash, meaning we can never accidentally break production without a traceable revision history.
