# 🌐 Phase 2 — Asset Discovery

Asset Discovery is the process of **finding every digital asset owned by the target organization**.

Most beginners only test:

https://example.com

But real organizations have **hundreds or thousands of assets**.

Example:

example.com  
api.example.com  
admin.example.com  
dev.example.com  
staging.example.com  
cdn.example.com  
blog.example.com  
payments.example.com

Every one of these can contain vulnerabilities.

So the goal is simple:

> **Find every asset before testing for vulnerabilities.**

---

# 🎯 Objectives of Asset Discovery

This phase answers key questions:

1. What **subdomains** exist?
    
2. What **APIs** exist?
    
3. What **servers and IPs** belong to the company?
    
4. What **cloud assets** exist?
    
5. What **hidden or forgotten services** exist?
    

This creates the **attack surface**.

More assets = more chances for vulnerabilities.

---

# 🧠 Why This Phase Is Powerful

Many bug bounty hunters find vulnerabilities **not on the main website** but on:

- old subdomains
    
- staging environments
    
- forgotten developer tools
    
- internal APIs accidentally exposed
    

Example:

dev.company.com  
staging.company.com  
beta.company.com  
old-api.company.com

Developers often forget to secure these.

---

# 🔎 Step 1 — Subdomain Enumeration

Subdomain enumeration means discovering domains like:

api.company.com  
admin.company.com  
mail.company.com  
vpn.company.com  
portal.company.com

These represent **separate applications**.

---

# ⚙️ Common Tools Used by Researchers

### Subfinder

Fast passive subdomain discovery.

subfinder -d example.com

---

### Amass

More advanced enumeration.

amass enum -passive -d example.com

---

### Assetfinder

assetfinder example.com

---

# 🧪 Example Workflow

Researchers often combine tools.

Example:

subfinder -d example.com >> subs.txt  
assetfinder example.com >> subs.txt  
amass enum -passive -d example.com >> subs.txt

Now we have a **large list of subdomains**.

Example output:

api.example.com  
dev.example.com  
cdn.example.com  
blog.example.com  
admin.example.com

---

# ⚙️ Step 2 — Verify Which Domains Are Alive

Not every discovered domain is active.

We test using **httpx**.

cat subs.txt | httpx

Example output:

https://api.example.com  
https://admin.example.com  
https://dev.example.com

Now we know **which servers respond**.

---

# 📡 Step 3 — Discover IP Infrastructure

We can identify the IP addresses behind domains.

Example tool:

dnsx

cat subs.txt | dnsx

Output:

api.example.com → 104.21.x.x  
admin.example.com → 172.67.x.x

Now we know **where servers are hosted**.

---

# ☁️ Step 4 — Cloud Asset Discovery

Many companies use cloud services like:

- AWS
    
- Azure
    
- Google Cloud
    

Cloud services create additional assets like:

company-assets.s3.amazonaws.com  
company-backups.s3.amazonaws.com  
company-storage.s3.amazonaws.com

Sometimes these buckets are **publicly accessible**.

Example breach scenario:

/backup.zip  
/users.csv  
/internal-logs.txt

This happens **very often**.

---

# 📜 Step 5 — Certificate Transparency Logs

SSL certificates expose subdomains.

Example service:

crt.sh

Search:

%.example.com

Results might reveal:

api.example.com  
vpn.example.com  
internal.example.com  
staging.example.com

Even **hidden environments**.

---

# 📊 Step 6 — Build the Asset List

After discovery we organize assets like:

ROOT DOMAIN  
│  
├── example.com  
│  
├── api.example.com  
├── dev.example.com  
├── staging.example.com  
├── admin.example.com  
├── blog.example.com

This becomes the **attack surface map**.

---

# ⚠️ Important Mindset

Think like this:

More assets = more bugs

Most beginners attack **one domain**.

Professional hunters attack **entire ecosystems**.

---

# 🧠 Example Real Recon Pipeline

Many hunters automate reconnaissance like this:

subfinder → assetfinder → amass  
      ↓  
     sort  
      ↓  
     httpx  
      ↓  
     naabu  
      ↓  
     nuclei

This pipeline can scan **thousands of assets automatically**.

---

# 📚 What Your Note Should Look Like in Obsidian

Title:

02 — Asset Discovery

Sections:

1. Objectives  
2. Subdomain Enumeration  
3. Alive Domain Verification  
4. Infrastructure Discovery  
5. Cloud Asset Discovery  
6. Certificate Transparency  
7. Asset Mapping

---

# ⚔️ Next Phase (Where Real Hacking Begins)

After assets are discovered we move to:

Phase 3 — Attack Surface Mapping

Where we find:

- endpoints
    
- APIs
    
- parameters
    
- hidden routes
    

Example:

/api/v1/login  
/api/v1/user/update  
/api/v1/payment/process

These endpoints are where **real vulnerabilities appear**.