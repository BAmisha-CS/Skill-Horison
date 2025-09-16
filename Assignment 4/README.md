# Web Application Recon & Scanning — Kali Linux Pentest
This project involves a **methodical web application assessment** using Kali Linux tools, targeting **authorized environments only**, such as:

- `zero.webappsecurity.com`
- `testphp.vulnweb.com`
- `testfire.net`

> **Important:** Unauthorized scanning of public websites is illegal and unethical. Only test systems that you own or have clear written permission to assess.

## Tools Used
| Purpose                    | Tool                           |
| -------------------------- | ------------------------------ |
| Network Scanning           | `nmap`                         |
| Web Fingerprinting         | `whatweb`, `wappalyzer`        |
| Directory Discovery        | `dirb`, `gobuster`             |
| Web Vulnerability Scanning | `nikto`, `OWASP ZAP`, `nuclei` |
| CMS Scanning (WordPress)   | `wpscan`                       |

## Steps Performed
### Step 1: Recon & Discovery
#### 1.1 Network Discovery using Nmap
```
nmap -sS -sV -T4 -Pn -oN nmap_scan.txt zero.webappsecurity.com
```
`-sS`: SYN scan (stealth)
`-sV`: Detect service versions
`-T4`: Faster execution
`-Pn`: Treat host as online
`-oN`: Output to file

#### 1.2 Web Fingerprinting
```
whatweb http://zero.webappsecurity.com > whatweb.txt
```
Or, if you prefer browser extension data:
Use Wappalyzer (browser extension) to detect frameworks, CMS, JavaScript libraries, etc.

#### 1.3 Directory Discovery using DIRB
```
dirb http://zero.webappsecurity.com /usr/share/wordlists/dirb/big.txt -o dirb_zero.txt
```
### Step 2: Light Automated Scans
#### 2.1 Nikto Scan
```
nikto -h http://zero.webappsecurity.com -output nikto.txt
```
**Scans for:** - HTTP misconfigurations
              - Outdated server software
             - Dangerous files and directories

#### 2.2 Nuclei Scan
```
nuclei -u http://zero.webappsecurity.com -as -o nuclei.txt -c 10
```
`-as`: Enable automatic severity-based filtering
`-c 10`: Use 10 concurrent threads

#### 2.3 OWASP ZAP Baseline Scan
```
zap-baseline.py -t http://zero.webappsecurity.com -r zap_baseline.html
```
Passive scan only (safe)
Generates report: `zap_baseline.html`

#### 2.4 WPScan (Only if WordPress Detected)
```
wpscan --url http://target.com --enumerate vp,vt,cb,dbe,u --api-token YOUR_TOKEN -o wpscan.txt
```
**Detects:** - Vulnerable plugins/themes
             - User enumeration
             - Known CVEs

## Project Structure
project/
├── nmap_scan.txt
├── whatweb.txt
├── dirb_zero.txt
├── nikto.txt
├── nuclei.txt
├── zap_baseline.html
├── wpscan.txt (if applicable)
└── README.md

## Notes
- Always verify tool paths and ensure wordlists are available `(/usr/share/wordlists/)`
- For faster scans or recursion, consider replacing `dirb` with `gobuster` or `ffuf






















