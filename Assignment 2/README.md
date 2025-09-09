#  Passive Footprinting & Reconnaissance

##  Objective
The goal of this project is to gather **publicly available information** about a target without actively interacting with its systems. This foundational phase of penetration testing and ethical hacking reveals what an attacker can learn about a system before any direct engagement.

## Repository Structure
The repository is organized to allow easy navigation and replication of steps:

Passive-Footprinting-And-Recon/
├── README.md         # Main Report for this target
├── 01.Domain_Information_gathering.md
├── 02.Subdomains_enumeration.md
├── 03.Email_And_Emloyee_Info.md
├── 04.Metadata_Extraction.md
├── 05.Google_dorking.md
├── 06.Social_media_&_OSINT.md
├── 
├── outputs/               # Raw outputs of commands
│   ├── whois.txt
│   ├── dig.txt
│   ├── nslookup.txt
│   ├── final_subdomains.txt
│   ├── dorks.txt
│   ├── emails.txt
│   ├── urls.txt
│   ├── jsfiles.txt
│   └── metadata.txt ....
└── screenshots/           # Screenshots of each step
    ├── 01_domaininfo.png
    ├── 02_subs.png
    ├── 03_emails.png
    ├── 04_metadata.png
    ├── 05_dorking.png
    └── 06_urls_js.png ....
```
##  Tools Used
- `whois`, `dig`, `nslookup` → Domain & DNS details
- `subfinder`, `assetfinder`, `amass` (passive) → Subdomain enumeration
- `theHarvester` → Public email & employee info
- `metagoofil`, `exiftool` → Metadata extraction from public documents
- `Google Dorking` → Search engine-based reconnaissance
- `gau`, `katana`, `linkfinder` → Collect URLs & JS files
- `JSLeak` → Search secrets in JS files
- `Maltego (CE)` / `SpiderFoot` → OSINT automation (optional)

##**Steps Performed:**

## 1. Domain Information Gathering
**Commands:**
```bash
whois yahoo.com > whois.txt
dig yahoo.com  > dig.txt
nslookup yahoo.com > nslookup.txt
```
Purpose: Collect domain registrar details, DNS records, and IP addresses.

### 2.. Subdomain Enumeration
**Commands:**
```bash
subfinder -d yahoo.com -o subfinder_yahoo.txt
assetfinder yahoo.com > assetfinder_yahoo.txt
amass enum -passive -d yahoo.com > amass_yahoo.txt
```
Purpose: Identify publicly accessible subdomains that could expose staging environments, APIs, or forgotten assets.

### 3️.. Email & Employee Information
**Command:**
```bash
theHarvester -d yahoo.com -b google,bing,linkdln > yahoo_emails.txt
```
Purpose: Extract public email addresses and employee information which may be leveraged in phishing or social engineering.

### 4️.. Metadata Extraction
**Commands:**
```bash

exiftool sample.pdf >> outputs/metadata.txt
```
Purpose: Retrieve metadata such as author names and software details from public documents to gather insights into internal systems or user identities.

### 5️.. Google Dorking
**Queries Tried:**
```
site:yahoo.com filetype:pdf
site:yahoo.com inurl:admin
site:yahoo.com intitle:index of
```
Purpose: Locate exposed files, directories, admin portals, and sensitive information indexed by search engines.

### 6.. Social Media & OSINT (Optional)
**Tools:** Maltego CE / SpiderFoot
Purpose: Map the organization’s public presence, including LinkedIn employees, Twitter accounts, and GitHub repositories.

### 7..7️URLs & JS Files
**Commands:**
```bash
gau yahoo.com > yahoo_urls.txt
cat outputs/urls.txt | grep "\.js" > yahoo_jsfiles.txt
```
Purpose: Map the organization’s public presence, including LinkedIn employees, Twitter accounts, and GitHub repositories.
---

##**Conclusion: Possible Attack Surfaces Identified:**

Passive reconnaissance of yahoo.com revealed:

* Subdomains & URLs: Multiple active subdomains such as 2013-en-imagenes.es.yahoo.com, admin.nevec.yahoo.com, and admanager.yahoo.com, which represent potential entry points.
* Domain & DNS Info: Presence of multiple authoritative name servers, IPv4/IPv6 addresses, and mail exchange records indicating robust hosting infrastructure.
* Emails / Employee Info: No publicly exposed employee emails were found; document metadata showed company authorship with no sensitive internal paths.
* OSINT / Public Profiles: Limited exposure, with only 4 LinkedIn profiles and 2 GitHub repositories linked to the organization.

  
Key Takeaway: While public information was limited, passive reconnaissance successfully identified external assets and highlighted the organization's strong security posture with minimal sensitive data exposure.
