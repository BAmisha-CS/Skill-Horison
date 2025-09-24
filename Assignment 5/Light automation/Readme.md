# DVWA Light Automation Scanning

This repository documents the use of light, fast, and effective web security automation tools against a local instance of **DVWA (Damn Vulnerable Web Application)** running at `http://127.0.0.1`.

The goal is to perform initial reconnaissance, content discovery, fingerprinting, and basic vulnerability scanning using command-line tools.

## Target

- **DVWA Instance**: `http://127.0.0.1`
- **Target File**: `dvwa.txt`
  
# dvwa.txt
http://127.0.0.1

## Tools Used
| Tool        | Purpose                                |
| ----------- | -------------------------------------- |
| **Dirb**    | Directory and file enumeration         |
| **WhatWeb** | Web technology fingerprinting          |
| **Nikto**   | Web server vulnerability scanning      |
| **Nuclei**  | Template-based vulnerability detection |

## Commands Used
1. **Dirb** — Directory & File Bruteforce
Scans the web root for common files and directories using a predefined wordlist.

`dirb http://127.0.0.1 /usr/share/wordlists/dirb/common.txt -o dirb_dvwa.txt`

- **Wordlist used**: common.txt
- **Output file**: dirb_dvwa.txt

  **Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%205/Light%20automation/Dirb.png">
</p>

2. **WhatWeb** — Web Technology Fingerprinting
Identifies technologies and platforms used by the target web application.

`whatweb -v http://127.0.0.1`

- **Verbose Mode**: Shows detailed plugin results
- Output is typically printed to terminal, redirect if needed:
  
`whatweb -v http://127.0.0.1 > whatweb_dvwa.txt`

**Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%205/Light%20automation/whatweb.png">
</p>

3. **Nikto** — Web Server Vulnerability Scanner
Scans for outdated software, dangerous options, and basic misconfigurations.

`nikto -h http://127.0.0.1 -output nikto_dvwa.txt`

- **Host**: Local DVWA
- **Output file**: `nikto_dvwa.txt`

  **Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%205/Light%20automation/Nikto.png">
</p>

 4. **Nuclei** — Vulnerability Scanner
Uses predefined templates to find misconfigurations, exposed files, and known CVEs.

`nuclei -u http://127.0.0.1/dvwa -o ~/nuclei_dvwa.txt`

- **Target Path**:` /dvwa`
- **Output File**:` ~/nuclei_dvwa.txt (home directory)`
- **To scan with specific templates**: `nuclei -u http://127.0.0.1/dvwa -t vulnerabilities/ -o ~/nuclei_dvwa.txt`

  **Screenshot:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%205/Light%20automation/nuclei.png">
</p>

## Output Files
All tools output to the following files:
├── dvwa.txt                 # Target list
├── dirb_dvwa.txt            # Dirb results
├── nikto_dvwa.txt           # Nikto results
├── whatweb_dvwa.txt         # (If redirected)
└── nuclei_dvwa.txt          # Nuclei results


**Legal & Ethical Notice**
*This project is for educational purposes only. You must only scan systems that you own or have explicit permission to test. Unauthorized scanning is illegal and unethical.*
