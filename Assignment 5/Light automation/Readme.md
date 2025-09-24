# DVWA Light Automation Scanning

This repository documents the use of light, fast, and effective web security automation tools against a local instance of **DVWA (Damn Vulnerable Web Application)** running at `http://127.0.0.1`.

The goal is to perform initial reconnaissance, content discovery, fingerprinting, and basic vulnerability scanning using command-line tools.

## 🎯 Target

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

2. **WhatWeb** — Web Technology Fingerprinting
Identifies technologies and platforms used by the target web application.
`whatweb -v http://127.0.0.1`
- **Verbose Mode**: Shows detailed plugin results
- Output is typically printed to terminal, redirect if needed:
`whatweb -v http://127.0.0.1 > whatweb_dvwa.txt`

3. **Nikto** — Web Server Vulnerability Scanner
Scans for outdated software, dangerous options, and basic misconfigurations.
`nikto -h http://127.0.0.1 -output nikto_dvwa.txt`
- **Host**: Local DVWA
- **Output file**: `nikto_dvwa.txt`

 4. **Nuclei** — Vulnerability Scanner
Uses predefined templates to find misconfigurations, exposed files, and known CVEs.
`nuclei -u http://127.0.0.1/dvwa -o ~/nuclei_dvwa.txt`


Target Path: /dvwa

Output File: ~/nuclei_dvwa.txt (home directory)

To scan with specific templates:

nuclei -u http://127.0.0.1/dvwa -t vulnerabilities/ -o ~/nuclei_dvwa.txt
