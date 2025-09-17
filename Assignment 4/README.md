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

**Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/nmap.png"></p>

#### 1.2 Web Fingerprinting
```
whatweb http://zero.webappsecurity.com > whatweb.txt
```
Or, if you prefer browser extension data:
Use Wappalyzer (browser extension) to detect frameworks, CMS, JavaScript libraries, etc.

**Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/whatweb.png"></p>

#### 1.3 Directory Discovery using DIRB
```
dirb http://zero.webappsecurity.com /usr/share/wordlists/dirb/small.txt -o dirb.txt
```

**Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/Dirb.png"></p>

### Step 2: Light Automated Scans
#### 2.1 Nikto Scan
```
nikto -h http://zero.webappsecurity.com -output nikto.txt
```
**Scans for:** - HTTP misconfigurations
              - Outdated server software
             - Dangerous files and directories

**Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/Nikto.png"></p>             

#### 2.2 Nuclei Scan
```
nuclei -u http://zero.webappsecurity.com -as -o nuclei.txt -c 10
```
`-as`: Enable automatic severity-based filtering
`-c 10`: Use 10 concurrent threads

**Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/Nuclei.png"></p>

#### 2.3 OWASP ZAP Baseline Scan
```
sudo docker run -v $(pwd):/zap/wrk/:rw --network="host" ghcr.io/zaproxy/zaproxy:stable zap-baseline.py -t http://zero.webappsecurity.com -r zap_baseline.html
```

**Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/OWASP_ZAP.png"></p>

<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/ZAP_Baseline_Scanning.png"></p>

**Scans for:** - Passive vulnerabilities (e.g. missing security headers, cookie flags)
               - Crawls the target site using spiders
               - Generates a clean HTML report (zap_baseline.html) in your current directory
               - Safe for production (does not perform active attacks)
> **Make sure Docker is installed and running. This command uses the official ZAP Docker image.**

#### 2.4 WPScan (Only if WordPress Detected)
```
wpscan --url http://zero.webappsecurity.com --enumerate vp,vt,cb,dbe,u --api-token YOUR_TOKEN -o wpscan.txt
```
**Detects:** - Vulnerable plugins/themes
             - User enumeration
             - Known CVEs

             **Screenshot:**
<p align="center"><img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%204/Screenshots/WPScan.png"></p>

## Project Structure
project/
├── nmap_scan.txt
├── whatweb.txt
├── dirb_zero.txt
├── nikto.txt
├── nuclei.txt
├── OWASP ZAP Baseline Scan
├── wpscan.txt (if applicable)
└── README.md

## Notes
- Always verify tool paths and ensure wordlists are available `(/usr/share/wordlists/)`
- For faster scans or recursion, consider replacing `dirb` with `gobuster` or `ffuf





