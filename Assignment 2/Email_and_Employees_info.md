 
#  3: Email & Employee Information Gathering (theHarvester)

### Objective :
The goal of this step is to gather publicly available **emails, employee names, and related hosts** for the target domain.  
This information can be useful in:
- **Social engineering attacks** (like phishing)
- **Username format discovery** (for brute-force attacks)
- **OSINT investigations** (knowing who works at the company)

---

###  Command Used

```bash
theHarvester -d yahoo.com -l 100 -b bing,duckduckgo,yahoo,linkedin > heharvester_yahoo.txt
````

* `-d yahoo.com` → target domain
* `-l 100` → limit to the first 100 results from each source
* `-b` → sources to use (bing, duckduckgo, yahoo, crtsh, linkedin)
* `> outputs/theharvester_yahoo.txt` → saves output to a text file for later review

---

### Output: 
[theharvester_yahoo.txt](https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%202/Output/theharvester_yahoo.txt)

**No emails, names, or hosts were found for yahoo.com.**
This is common for large companies because they usually implement measures to prevent employee data from being exposed online.

**Screenshots:**
<p align="center">
  <img src="https://github.com/BAmisha-CS/Skill-Horison/blob/main/Assignment%202/Screenshots/theharvester_yahoo.txt.png" width="80%">
</p>
---

###  Key Takeaways

* No publicly available employee emails were found.
* This reduces the risk of phishing attacks against the organization.
* Even "no result" is a valuable finding — it shows good security posture.

---
