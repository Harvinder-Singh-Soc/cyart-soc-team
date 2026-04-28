# Task 1: Threat Hunting Practice

## Objective
Proactive threat hunting using hypothesis-driven methodology to detect potential abuse of privileged account assignments in a Windows environment.

---

## Lab Setup

| Component | Details |
|-----------|---------|
| **SIEM / Log Analysis** | Elastic Stack (Kibana) – `192.168.56.101:5601` |
| **Log Shipper** | Elastic Agent (Filebeat) on Windows endpoint |
| **Endpoint** | Window-Endpoint (Windows 10) |
| **Audit Policy** | Special Logon auditing enabled via `auditpol.exe` |
| **Data View** | `window-security` |

---

## Hypothesis

**"An adversary may be abusing valid accounts by assigning special privileges to escalate access or maintain persistence."**

- **MITRE ATT&CK Mapping:** T1078 – Valid Accounts
- **Event Targeted:** Windows Event ID 4672 – Special Privileges Assigned to New Logon

**Rationale:** Attackers often escalate privileges or assign special rights to compromised accounts to maintain persistence or move laterally. Monitoring Windows Event ID 4672 helps detect such privilege assignments.

---

## Methodology (SqRR Framework)

### 1. Search
- Opened Kibana at `http://192.168.56.101:5601`
- Navigated to **Discover**
- Selected the `window-security` data view
- Set time range: April 28, 2026

### 2. Query
Executed the following KQL query:
agent.name: "Window-Endpoint" AND event.code: "4672"


### 3. Retrieve
Query returned **16 matching documents** spanning the day.

**Representative findings:**

| Timestamp | Agent | Event Code | Dataset | Event Action |
|-----------|-------|------------|---------|--------------|
| 2026-04-28 12:09:28 | Window-Endpoint | 4672 | system.security | logged-in |
| 2026-04-28 12:13:48 | Window-Endpoint | 4672 | system.security | logged-in |
| 2026-04-28 12:18:39 | Window-Endpoint | 4672 | system.security | logged-in |
| 2026-04-28 12:18:41 | Window-Endpoint | 4672 | system.security | logged-in |
| 2026-04-28 12:29:27 | Window-Endpoint | 4672 | system.security | logged-in |
| 2026-04-28 12:29:28 | Window-Endpoint | 4672 | system.security | logged-in |
| 2026-04-28 12:44:42 | Window-Endpoint | 4672 | system.security | logged-in |

**Screenshot:** *(Kibana Discover showing 16 matching events with field details)*

### 4. Respond
All observed events must be correlated with authorized administrative activities. Any privilege assignment not matching an approved change window or administrative task should trigger an incident response process, including:
- Account verification
- Session investigation
- Possible containment

---

## MITRE ATT&CK Mapping

| Technique ID | Technique Name | Description |
|--------------|----------------|-------------|
| T1078 | Valid Accounts | Adversaries may use valid accounts to gain initial access or escalate privileges. Event 4672 logs the assignment of special privileges, which could indicate misuse. |

---

## Observations

- **16 events** observed throughout the day
- All originated from `Window-Endpoint` (IP: 192.168.56.150)
- Normal pattern for an active Windows system with regular administrative tasks:
  - Running programs as Administrator
  - Scheduled tasks executing with elevated privileges
  - System services performing privileged operations
- In a real SOC environment, each event's `SubjectUserName` and `PrivilegeList` fields would be examined for anomaly detection

---

## Tools & Technologies Used

| Tool | Purpose |
|------|---------|
| **Elastic Stack (Kibana)** | Log analysis, visualization, and threat hunting |
| **Elastic Agent (Filebeat)** | Log collection and forwarding from Windows endpoint |
| **Windows 10 Endpoint** | Source of security events (Event ID 4672) |
| **MITRE ATT&CK Framework** | Reference for adversary tactics and techniques |

---

## Skills Demonstrated

- ✅ Hypothesis-driven threat hunting
- ✅ KQL (Kibana Query Language) usage
- ✅ Windows security event analysis
- ✅ MITRE ATT&CK framework application
- ✅ Elastic Security for SOC operations
- ✅ Audit policy configuration

---

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Event 4672 not appearing initially | Enabled **Special Logon** audit policy using `auditpol.exe /set /subcategory:"Special Logon" /success:enable /failure:enable` |
| Large volume of events | Narrowed query using KQL filters (`agent.name` + `event.code`) |
| Understanding event fields | Explored `SubjectUserName` and `PrivilegeList` fields to understand privilege assignments |

---

## Conclusion

The threat hunting exercise was completed successfully. Kibana Elastic Security proved effective for querying Windows security logs in near real-time. The presence of multiple Event 4672 logs demonstrates the normal occurrence of this event during legitimate administrative activity. However, the process of isolating and investigating these events constitutes the foundation of a proactive SOC threat hunting workflow.

**Key Takeaway:** This method can identify privileged session creation. When combined with continuous monitoring and correlation with PAM (Privileged Access Management) logs, it becomes a powerful detection technique against credential abuse.

---

## Lessons Learned

1. Audit policy must be **explicitly enabled** for Event 4672 to appear in logs
2. Kibana Discover provides **rapid ad-hoc hunting** capabilities
3. Combining **MITRE ATT&CK** with specific Event IDs creates focused, efficient hunts
4. Elastic Agent (Filebeat) reliably ships Windows security logs to Elasticsearch
5. Proper field mapping (`agent.name`, `event.code`) enables precise querying

---

**Status:** ✅ Complete  
**Date:** April 28, 2026  
**Analyst:** [Your Name]

---

**Screenshot Reference:** `screenshots/kibana_hunt_4672.png`