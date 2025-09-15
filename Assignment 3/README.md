# Active Reconnaissance Report Guide

> **IMPORTANT:** All scanning and enumeration tasks were performed only on **authorized targets** (e.g., `testfire.net`, `testphp.vulnweb.com`, `zero.webappsecurity.com`) in compliance with ethical hacking lab rules.

## Tools Used

| Tool     | Purpose                                                                 |
|----------|-------------------------------------------------------------------------|
| `nmap`   | Host discovery, port scanning, service/version detection, OS fingerprinting |
| `dirb`   | Brute-force directory and file enumeration on web servers               |
| `whatweb`| Web application fingerprinting                                          |
| `nikto`  | Web vulnerability scanner                                               |

## Step 1: Host Discovery
### Objective
Check if the target is live and identify its IP address.
```bash
nmap -sn testfire.net
```
### Explanation
**`-sn`**: Ping Scan only (no port scanning)  
Used to determine if the host is online and reachable.

**Output**
Nmap scan report for testfire.net (192.168.1.10)
Host is up (0.056s latency).

**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/Host_Discovery.png">
</p>

## Step 2: Port & Service Scanning (Nmap)
### 2.1 TCP SYN Scan (Quick Port Scan)
```bash
nmap -sS testfire.net
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/TCP_SYN_SCAN.png">
</p>

-sS: TCP SYN scan (stealthy and fast)
Scans top 1000 common ports
Quick way to discover open ports

### 2.2 Common Ports + NSE Script Scan
```bash
nmap -sV -p 22,80,443 -sC testfire.net
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/Service_Version_Scan(common%20ports).png">
</p>

-p 22,80,443: Scan only SSH, HTTP, HTTPS
-sV: Service version detection
-sC: Run default Nmap scripts (e.g., banner grabbing, HTTP checks)

### 2.3 Full Port Scan (Alternative Syntax)
```bash
nmap -sV -p- testfire.net
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/full_port_scan.png">
</p>

-p-: Shortcut for all ports (1–65535)
Use this if -p1-65535 seems slower

### 2.4 OS Detection
```bash
nmap -O --osscan-guess testfire.net
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/OS_Detection.png">
</p>

-O: Enable OS detection
--osscan-guess: Make a best guess when OS fingerprinting is uncertain
May not always be allowed or accurate

## Step 3: HTTP Enumeration with dirb
```bash
dirb http://testfire.net
dirb http://testfire.net /usr/share/wordlists/dirb/common.txt
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/HTTP_Enumeration_dirb.png">
</p>

**Explanation**
Performs brute-force directory/file enumeration on the web server
Useful for finding admin panels, login pages, hidden resources

## Step 4: Web Fingerprinting & Vulnerability Scanning
### 4.1 WhatWeb
```bash
whatweb http://testfire.net
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/whatweb.png">
</p>

### 4.2 Nikto Scan
```bash
nikto -h http://testfire.net -o nikto.txt
```
**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%203/Screenshots/nikto.png">
</p>

## Deliverables Checklist

|  Section               |  Description                                                             |
|--------------------------|-----------------------------------------------------------------------------|
| Host Discovery           | IP address of the target and whether it is up                              |
| Nmap Outputs             | Screenshots/snippets from each scan type                                   |
| Open Ports & Services    | List of open ports, detected services, version info, and confidence level  |
| NSE Script Findings      | Summarized output of important script results                               |
| Dirb Output              | List of discovered directories and files from `dirb`                        |
| WhatWeb & Nikto          | Web server technologies and known vulnerabilities                          |

##  Notes & Best Practices
- Start with quick scans, then perform deeper ones if needed.
- Use `-oN output.txt` in Nmap to save results to a file.
- Validate findings — not all open ports are exploitable.
- Be ethical and scan only authorized targets.

## Sample Folder Structure for Submission
active-recon-report/
├── README.md
├── host_discovery.txt
├── nmap/
│   ├── quick_scan.txt
│   ├── full_port_scan.txt
│   ├── service_scan.txt
│   └── os_detection.txt
├── dirb/
│   ├── dirb_default.txt
│   └── dirb_common.txt
├── nikto/
│   └── nikto.txt
├── whatweb/
│   └── whatweb.txt

## Key Learnings
- Understood the importance of staged scanning: starting with quick scans and moving to full-range, deeper scans.
- Learned how to identify live hosts using Nmap’s `-sn` option.
- Gained hands-on experience with various Nmap scan types:
  - TCP SYN scan (`-sS`)
  - Service & version detection (`-sV`)
  - Default NSE script execution (`-sC`)
  - OS detection (`-O`)
- Explored HTTP enumeration using `dirb` to discover hidden directories and files.
- Used `whatweb` for fingerprinting web technologies and `nikto` for basic web vulnerability scanning.
- Reinforced the importance of ethical hacking — scanning only authorized targets.

## Conclusion
- Performed active reconnaissance using authorized tools and techniques.
- Identified live hosts and discovered open ports and running services.
- Used Nmap for staged scanning, version detection, and script analysis.
- Enumerated web directories and files using `dirb`.
- Fingerprinted web technologies with `whatweb` and scanned for vulnerabilities using `nikto`.
- Ensured all activities were within ethical and legal boundaries.
- Strengthened core skills in network scanning, service enumeration, and web reconnaissance.

