# Subdomain Enumeration Assignment

## Overview

This folder contains the complete work for the assignment focused on subdomain enumeration.

**Task:**  
Collect subdomains of two different targets using three distinct tools/scripts.

Subdomain enumeration is a critical first step in bug bounty hunting and penetration testing, aimed at uncovering hidden subdomains associated with a target website. In this assignment, I utilized a combination of tools to discover subdomains, generate permutations, and verify which ones are alive.

## Contents

- **Target 1:** `testphp.vulnweb.com` (Practice target) — [`Tesphp.vulnweb.md`](Tesphp.vulnweb.md)  
- **Target 2:** `hackerone.com` (Practice target) — [`Hackerone.md`](Hackerone.md)  

Each target folder includes:  
- Commands executed and output files  
- Screenshots of results  
- Final list of live subdomains  

## Tools Used

| Tool       | Purpose                                 |
|------------|-----------------------------------------|
| **Subfinder**   | Finds verified real subdomains         |
| **Assetfinder** | Discovers additional subdomains        |
| **AlterX**      | Generates permutations and guesses      |
| **Dnsx**        | Filters and probes only live subdomains |

## Key Learnings
- Combining multiple tools results in more comprehensive subdomain coverage.  
- `dnsx` effectively filters out inactive subdomains, focusing analysis on live targets.  
- The methodology is reusable and adaptable for enumerating subdomains of any future domain.
- Combining multiple tools results in more comprehensive subdomain coverage.  
- `dnsx` effectively filters out inactive subdomains, focusing analysis on live targets.  
- The methodology is reusable and adaptable for enumerating subdomains of any future domain.
