# 🌐 Plain-English DNS & CNAME Walkthrough

**Track:** General AI Fluency  
**File:** `work/dns_walkthrough.md`  

---

### 1. What DNS Does (The Phonebook Analogy)
Computers only understand numeric IP addresses like `75.2.60.5`. Humans only remember friendly names like `google.com` or `rafayyk7.github.io`. 

The **Domain Name System (DNS)** is the internet's phonebook. It translates human names into computer IP addresses so your browser knows which exact server in the world to call.

---

### 2. What Happens When You Type a Website Address
When someone types your website address into a browser, four steps happen in under 50 milliseconds:

1. **The Resolver (The Assistant):** Your browser asks your internet provider's DNS resolver: *"What is the IP for this website?"*
2. **The Root Server (The Directory):** If the resolver doesn't know, it asks the Root server, which points it to the correct extension (like `.com` or `.io`).
3. **The TLD Server (The Registry):** The extension server points to the company hosting your domain's records (e.g., GitHub or Netlify).
4. **The Authoritative Nameserver (The Final Answer):** Netlify/GitHub answers with the exact server IP. Your browser connects to that IP and loads the website over secure HTTPS.

---

### 3. What is a CNAME Record?
* An **A Record** points a name directly to a hardcoded number IP (e.g., `mysite.com` ➔ `75.2.60.5`).
* A **CNAME Record (Canonical Name)** points a name to **another name (an alias)** instead of a number.

**Why this matters:** When you connect a custom domain (like `www.abdulrafay.com`), you set a CNAME pointing to `rafayyk7.github.io`. If GitHub changes its server IPs in the background, your site never breaks because your domain points to their name, not their temporary IP.
