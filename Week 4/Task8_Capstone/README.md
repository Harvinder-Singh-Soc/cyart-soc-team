# Task 8: Capstone Project – Comprehensive SOC Incident Response

**Analyst:** SOC Analyst  
**Date:** April 28, 2026  
**Status:** Complete

---

## Objective
Simulate a full attack lifecycle – reconnaissance, exploitation, detection, automated triage, response, and post-incident analysis. Demonstrate end‑to‑end SOC capabilities using the integrated lab.

---

## Lab Setup (VMs Used)

| VM | IP | Role |
|----|----|------|
| Kali Attacker | 192.168.56.170 | Attack machine |
| Metasploitable2 | 192.168.56.140 | Vulnerable target (Samba) |
| Wazuh Manager | 192.168.56.100 | SIEM – alert generation |
| TheHive | 192.168.56.110:9000 | Case management (automated) |
| Windows Endpoint | 192.168.56.150 | Additional monitoring (Wazuh agent) |
| LabRouter | 192.168.56.1 | Gateway (optional, Snort available) |

---

## Attack Scenario
- **Attacker:** Kali Linux (192.168.56.170)
- **Target:** Metasploitable2 (192.168.56.140)
- **Vulnerability:** Samba `usermap_script` (CVE-2007-2447)
- **Method:** Nmap scan → Metasploit exploit → root access obtained

---

## Attack Timeline

| Time (UTC) | Event |
|------------|-------|
| 17:14 | Nmap reconnaissance detected (multiple rule 2551 alerts in Wazuh) |
| 17:16 | Metasploit Samba exploit executed, root shell gained |
| 17:18 | Wazuh alerts escalated (sudo to root, PAM session opened) |
| 23:02 | TheHive case automatically created via custom Wazuh integration |

---

## Detection & Response

- **SIEM Detection:** Wazuh triggered rule **2551 (level 10)** and other rules, clearly identifying the attack.
- **Automation:** The `custom-thehive` integration script instantly created case **#4 (~4312)** in TheHive with full alert details – **zero manual intervention**.
- **Triage (TheHive):**
  - Added observables: attacker IP (192.168.56.170), target IP (192.168.56.140), port 445, CVE-2007-2447.
  - Created tasks: Reconnaissance Detected, Exploitation Executed, Containment, RCA, Closure.
  - Marked all tasks completed.
  - Closed as **True Positive**.
- **Containment:** Attacker IP blocked (simulated). Metasploitable2 isolated (simulated).
- **Root Cause Analysis (5 Whys):**
  1. Why was server compromised? → Unpatched Samba vulnerability exploited.
  2. Why was it unpatched? → Legacy system, no regular patching.
  3. Why no patching? → No patch management policy for legacy servers.
  4. Why no policy? → Security not involved in legacy system lifecycle.
  5. Why not involved? → No formal asset management process.
  
  **Root Cause:** Lack of asset management and patch governance for legacy systems.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|--------|-----------|----|
| Reconnaissance | Network Service Scanning | T1046 |
| Exploitation | Exploitation of Remote Services | T1210 |
| Privilege Escalation | Abuse Elevation Control Mechanism | T1548 |
| Persistence (potential) | Valid Accounts (root session) | T1078 |

---

## Metrics

| Metric | Value | Notes |
|--------|-------|-------|
| **MTTD** | 0 seconds | Case auto‑created instantly on alert |
| **MTTR** | ~10 minutes | Manual triage & closure (could be automated further) |
| **Dwell Time** | ~4 minutes | First scan to root access |

---

## Stakeholder Briefing (150 words)

*During a routine security exercise, the SOC detected and responded to an attempted breach of a legacy server. An attacker scanned the network and exploited a known Samba vulnerability to gain root access. Our Wazuh SIEM immediately generated alerts, and our automated integration created a case in TheHive without any analyst intervention. The incident was contained within minutes, and a thorough root cause analysis was conducted. The vulnerability has been flagged for immediate patching. The successful detection and automatic response demonstrate our readiness to handle real‑world attacks efficiently. We continue to improve our automated playbooks to further reduce response times.*

---

## Screenshots

| File | Description |
|------|-------------|
| `nmap_scan.png` | Kali Nmap scan showing open Samba ports |
| `metasploit_exploit.png` | Metasploit exploit options and root shell |
| `wazuh_alerts.png` | Wazuh JSON alerts during attack |
| `wazuh_dashboard.png` | Wazuh dashboard with attack events |
| `thehive_case_auto.png` | TheHive case #4 created automatically |

---

## Repository Structure (Week 4)
