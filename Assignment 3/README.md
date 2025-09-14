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

### Command
```bash
nmap -sn testfire.net

**Explanation**

-sn: Ping Scan only (no port scanning)

Used to determine if the host is online and reachable

Sample Output
Nmap scan report for testfire.net (192.168.1.10)
Host is up (0.056s latency).

Step 2: Port & Service Scanning (Nmap)
2.1 TCP SYN Scan (Quick Port Scan)
nmap -sS testfire.net


-sS: TCP SYN scan (stealthy and fast)

Scans top 1000 common ports

Quick way to discover open ports

2.2 Common Ports + NSE Script Scan
nmap -sV -p 22,80,443 -sC testfire.net


-p 22,80,443: Scan only SSH, HTTP, HTTPS

-sV: Service version detection

-sC: Run default Nmap scripts (e.g., banner grabbing, HTTP checks)

2.3 Full Port Scan with NSE Scripts
nmap -sV -p1-65535 -sC testfire.net


Full port scan (1–65535) to find services running on non-standard ports

May take time to complete

2.4 Full Port Scan (Alternative Syntax)
nmap -sV -p- testfire.net


-p-: Shortcut for all ports (1–65535)

Use this if -p1-65535 seems slower

2.5 OS Detection
nmap -O --osscan-guess testfire.net


-O: Enable OS detection

--osscan-guess: Make a best guess when OS fingerprinting is uncertain

May not always be allowed or accurate

📝 Include in Report

✅ List of open ports

✅ Services detected on each port

✅ Version info (e.g., Apache 2.4.7)

✅ Confidence level (e.g., 90%)

✅ Summary of NSE script results (e.g., SSL cert info, default credentials, server config issues)

🌐 Step 3: HTTP Enumeration with dirb
3.1 Default Wordlist
dirb http://testfire.net

3.2 Custom Wordlist
dirb http://testfire.net /usr/share/wordlists/dirb/common.txt

📌 Explanation

Performs brute-force directory/file enumeration on the web server

Useful for finding admin panels, login pages, hidden resources

🧾 Sample Output
---- Scanning URL: http://testfire.net/ ----
+ http://testfire.net/admin/ (CODE:200|SIZE:345)
+ http://testfire.net/login/ (CODE:200|SIZE:781)
+ http://testfire.net/images/ (CODE:301|SIZE:0)

🕸 Step 4: Web Fingerprinting & Vulnerability Scanning
4.1 WhatWeb
whatweb http://testfire.net

📌 Sample Output
http://testfire.net [200 OK] Country[US], HTTPServer[Apache/2.4.7], IP[192.168.1.10], JQuery[1.9.1], PHP[5.4.16]

4.2 Nikto Scan
nikto -h http://testfire.net -o nikto.txt

📌 Sample Output
+ Server: Apache/2.4.7
+ Retrieved x-powered-by header: PHP/5.4.16
+ The X-XSS-Protection header is not defined.
+ Cookie JSESSIONID created without the HttpOnly flag.
+ OSVDB-877: Apache is vulnerable to a DoS via mod_deflate.

🗂️ Deliverables Checklist
Section	Description
✅ Host Discovery	IP address of the target and whether it is up
✅ Nmap Outputs	Screenshots/snippets from each scan type
✅ Open Ports & Services	List of open ports, detected services, version info, and confidence level
✅ NSE Script Findings	Summarized output of important script results
✅ Dirb Output	List of discovered directories and files from dirb
✅ WhatWeb & Nikto	Web server technologies and known vulnerabilities
🧠 Notes & Best Practices

Start with quick scans, then perform deeper ones if needed.

Use -oN output.txt in Nmap to save results to a file.

Validate findings — not all open ports are exploitable.

Be ethical and scan only authorized targets.

📁 Sample Folder Structure for Submission
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
