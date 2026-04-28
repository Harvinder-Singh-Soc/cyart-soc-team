# Week 4: SOC Team Practical Labs

**Team:** cyart-soc-team  
**Submission:** This repository (`cyart-soc-team/Week_4`)  
**Deadline:** April 24 – 5:30 PM

---

## Overview

Complete SOC operations simulation covering threat hunting, SOAR playbook development, alert triage, evidence collection, adversary emulation, metrics reporting, and a final capstone incident response. All exercises are performed on a self‑contained virtual lab with isolated networking.

---

## Lab Environment

| Virtual Machine | IP Address | Role |
|----------------|------------|------|
| LabRouter | 192.168.56.1 | Internet gateway, Snort IDS |
| Wazuh Manager | 192.168.56.100 | SIEM and log analysis |
| Elastic Stack | 192.168.56.101 | Optional SIEM (used in some tasks) |
| TheHive / Velociraptor | 192.168.56.110 | Case management & DFIR |
| MITRE Caldera | 192.168.56.130 | Adversary emulation |
| Metasploitable2 | 192.168.56.140 | Vulnerable target (no internet) |
| Windows 10 Endpoint | 192.168.56.150 | Monitored endpoint |
| Ubuntu Endpoint | 192.168.56.160 | Monitored endpoint |
| Kali Attacker | 192.168.56.170 | Attack simulation |

All VMs communicate over a Host‑only network (`192.168.56.0/24`). Only LabRouter has internet access (NAT) and it blocks Metasploitable2 from reaching the internet.

---

## Tasks & Documentation

Each task has its own subfolder with a `README.md`, a PDF report, and relevant screenshots. Additionally, **all screenshots for the entire Week 4 are collected in the shared [`screenshots/`](screenshots/) folder**.

| # | Task | Folder | Key Tools | Status |
|---|------|--------|-----------|--------|
| 1 | Threat Hunting | `Task1_Threat_Hunting/` | Elastic Security, Velociraptor | ✅ |
| 2 | SOAR Playbook Development | `Task2_SOAR_Playbook/` | TheHive, Wazuh | ✅ |
| 3 | Post‑Incident Analysis | `Task3_Post_Incident_Analysis/` | 5 Whys, Fishbone, Metrics | ✅ |
| 4 | Alert Triage with Automation | `Task4_Alert_Triage/` | Wazuh → TheHive integration | ✅ |
| 5 | Evidence Analysis | `Task5_Evidence_Analysis/` | Velociraptor, Chain of Custody | ✅ |
| 6 | Adversary Emulation | `Task6_Adversary_Emulation/` | MITRE Caldera, Elastic | ✅ |
| 7 | Metrics & Executive Reporting | `Task7_Metrics_Reporting/` | Kibana dashboard, Google Docs | ✅ |
| 8 | Capstone Project | `Task8_Capstone/` | Full attack cycle | ✅ |

---

## Central Screenshot Repository

All screenshots captured during the lab are placed in the [`Week_4/screenshots/`](screenshots/) folder for easy access. Each task folder also contains its own screenshots if you prefer a per‑task view.

**Screenshots list:**

| File | Task | Description |
|------|------|-------------|
| `kibana_hunt_4672.png` | 1 | Kibana Discover with Event ID 4672 |
| `case_creation.png` | 2 | TheHive case creation |
| `tasks_progress.png` | 2 | Playbook tasks in progress |
| `observables.png` | 2 | IOCs added |
| `case_closed.png` | 2 | Case closed as True Positive |
| `5_whys_analysis.png` | 3 | 5 Whys table |
| `fishbone_diagram.png` | 3 | Ishikawa diagram |
| `metrics_calculation.png` | 3 | MTTD/MTTR metrics |
| `ossec_config.png` | 4 | Wazuh integration block |
| `python_script.png` | 4 | Custom Python script |
| `manual_test.png` | 4 | Manual script test |
| `windows_command.png` | 4 | User creation on Windows |
| `thehive_case.png` | 4 | Auto‑created case in TheHive |
| `thehive_detail.png` | 4 | Auto‑case details |
| `velociraptor_collection.png` | 5 | Velociraptor collection summary |
| `netstat_data.png` | 5 | Netstat output rows |
| `chain_of_custody.png` | 5 | Chain of custody document |
| `agent_alive.png` | 6 | Caldera agent connected |
| `operation_running.png` | 6 | Operation steps running |
| `operation_completed.png` | 6 | Operation final status |
| `elastic_detection.png` | 6 | Elastic detection (4688 events) |
| `dashboard_metrics.png` | 7 | Kibana metrics dashboard |
| `executive_summary.png` | 7 | Executive report document |
| `nmap_scan.png` | 8 | Kali Nmap results |
| `metasploit_exploit.png` | 8 | Metasploit exploit and root shell |
| `wazuh_alerts.png` | 8 | Wazuh JSON alerts |
| `wazuh_dashboard.png` | 8 | Wazuh dashboard with attack events |
| `thehive_case_auto.png` | 8 | Automatically created case in TheHive |

---

## How to Use

1. Clone or download this repository.
2. Open the `Week_4` folder.
3. Read each task's `README.md` for a step‑by‑step explanation.
4. Refer to the `screenshots/` folder for visual evidence.
5. Review the `PDF` reports for polished, submission‑ready documentation.

---

## Final Status

**All 8 tasks completed successfully.**  
The lab demonstrated end‑to‑end SOC capabilities: proactive detection, automated response, forensic analysis, adversary simulation, and executive reporting – all in a fully isolated, repeatable virtual environment.

**Happy hunting!** 🕵️‍♂️