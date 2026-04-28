# Task 4: Alert Triage with Automation

**Analyst:** analyst1@th.local | **Date:** April 28, 2026 | **Status:** Complete

---

## Objective
Automated alert triage from Wazuh SIEM to TheHive using custom Python integration.

## Lab Setup
| Component | Detail |
|-----------|--------|
| SIEM | Wazuh Manager (192.168.56.100) |
| SOAR | TheHive 5.2 (192.168.56.110:9000) |
| Endpoint | Windows 10 (192.168.56.150) |
| Integration | Python script + Wazuh integration framework |

## Configuration Summary
- Generated API key for analyst1@th.local
- Added custom-thehive integration block in ossec.conf (level 7+)
- Python script reads Wazuh alerts, extracts fields, POSTs to TheHive API

## Test Results
- Manual test: `SUCCESS: Case created in TheHive`
- Live test: `net user realtest Pass123! /add` → Case auto-created (~4219032)

## Automation Workflow
Windows Event → Wazuh Agent → Wazuh Manager → Python Script → TheHive API → Case Created


## MITRE ATT&CK
T1136 - Create Account (Persistence)

## Screenshots
ossec_config.png | python_script.png | manual_test.png | windows_command.png | thehive_case.png | thehive_detail.png