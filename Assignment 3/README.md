# 🛡️ Active Reconnaissance Report Guide

> **IMPORTANT:** All scanning and enumeration tasks were performed only on **authorized targets** (e.g., `testfire.net`, `testphp.vulnweb.com`, `zero.webappsecurity.com`) in compliance with ethical hacking lab rules.

---

## 🛠 Tools Used

| Tool     | Purpose                                                                 |
|----------|-------------------------------------------------------------------------|
| `nmap`   | Host discovery, port scanning, service/version detection, OS fingerprinting |
| `dirb`   | Brute-force directory and file enumeration on web servers               |
| `whatweb`| Web application fingerprinting                                          |
| `nikto`  | Web vulnerability scanner                                               |

---

## 🔍 Step 1: Host Discovery

### ✅ Objective
Check if the target is live and identify its IP address.

### 📌 Command
```bash
nmap -sn testfire.net
```
### Explanation
**`-sn`**: Ping Scan only (no port scanning)  
Used to determine if the host is online and reachable.

Sample Output
Nmap scan report for testfire.net (192.168.1.10)
Host is up (0.056s latency).
