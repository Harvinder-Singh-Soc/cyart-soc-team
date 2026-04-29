# SOC Analyst Hands-on Training – Full Workflow Simulation

**Student:** Harvinder Singh  
**Date:** 29 April 2026  
**Deadline:** Friday, 5:30 PM

---

## 📌 Overview

This repository contains practical, hands-on labs covering the complete SOC (Security Operations Center) workflow.  
All tasks are performed on real virtual machines, using industry-standard tools.  
Each folder contains a dedicated `README.md` with step-by-step documentation and screenshots.

---

## 🛠️ Lab Environment

| Component | IP Address | Role |
|-----------|------------|------|
| Elastic Stack (Kibana) | 192.168.56.101 | Log Analysis & SIEM |
| Wazuh Server | 192.168.56.100 | Detection & Threat Intel |
| Windows Endpoint | 192.168.56.135 | Log source / Evidence |
| Kali Linux | 192.168.56.170 | Attacker machine |
| Metasploitable2 | 192.168.56.140 | Vulnerable target |
| TheHive | Docker | Case Management |
| Velociraptor Server | 192.168.56.110 | Forensic collection |

**Other Tools:** AlienVault OTX, VirusTotal, Google Docs, iptables, certutil

---

## 📚 Tasks Completed

| # | Task | Description | Status |
|---|------|-------------|--------|
| 1 | Advanced Log Analysis | Correlated Windows events, detected anomalies, enriched logs with GeoIP | ✅ |
| 2 | Threat Intelligence Integration | OTX feed import, MITRE-based alert enrichment, threat hunting | ✅ |
| 3 | Incident Escalation Workflows | TheHive case, SITREP draft, SOAR playbook | ✅ |
| 4 | Alert Triage with Threat Intel | Triage simulation, IOC validation via VirusTotal | ✅ |
| 5 | Evidence Preservation | Velociraptor netstat collection, chain of custody with SHA256 hash | ✅ |
| 6 | Capstone: Full SOC Simulation | Samba exploit, Wazuh detection, containment, escalation, reporting | ✅ |

Detailed documentation inside each folder.

---

## 📂 Repository Structure
SOC-Analyst-Training/
├── 1-Advanced-Log-Analysis/ # Log correlation, anomaly rule, GeoIP
├── 2-Threat-Intelligence/ # OTX, alert enrichment, threat hunting
├── 3-Incident-Escalation/ # TheHive case, SITREP, automation
├── 4-Alert-Triage/ # Triage table, VirusTotal validation
├── 5-Evidence-Preservation/ # Netstat collection, hash, chain of custody
├── 6-Capstone-Project/ # Full attack -> detect -> respond -> report
└── README.md # This file


---

## 🔍 Key Findings

- **Log Correlation:** Multiple Event ID 4625 followed by outbound 5156 to 8.8.8.8 = potential brute-force + C2 communication.
- **Threat Intelligence:** Wazuh enriched alerts automatically with MITRE ATT&CK T1078. OTX integration ready for real-time IP reputation checks.
- **Incident Handling:** TheHive case #6 escalated in < 5 minutes. SITREP and management briefing prepared.
- **Evidence:** Volatile data captured via Velociraptor. SHA256 hash maintained for file integrity.

---

## ⚙️ How to Use This Repo

1. Clone the repository.
2. Navigate to any task folder.
3. Open the `README.md` for that task to see full documentation.
4. Screenshots are inside the `screenshots/` subfolder.
5. Capstone project includes final PDF reports in `6-Capstone-Project/reports/`.

---

## 👤 Student Info

- **Name:** Harvinder Singh
- **Submission Date:** 29 April 2026
- **Tools Used:** Elastic Stack, Wazuh, TheHive, Velociraptor, Metasploit, CrowdSec/iptables, VirusTotal, AlienVault OTX

---

> **Disclaimer:** All tasks were performed in an isolated virtual lab environment. No production systems were used.