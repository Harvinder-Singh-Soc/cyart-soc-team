# Task 2: SOAR Playbook Development

## Objective
Design and execute a playbook for automated incident response to a phishing alert using TheHive SOAR platform. The goal is to simulate a real SOC analyst workflow from alert creation to containment and closure.

---

## Lab Setup

| Component | Details |
|-----------|---------|
| **SOAR Platform** | TheHive 5.2 – `http://192.168.56.110:9000` |
| **Organization** | SOC |
| **Analyst Account** | analyst1@th.local (Role: analyst) |
| **Admin Account** | admin@thehive.local (Role: org-admin) |
| **Scenario** | Phishing email with malicious attachment |

---

## Playbook Design: Phishing Incident Response

### Playbook Flowchart

┌──────────────────────────────┐
│ ALERT: Phishing Email │
│ (SIEM/Wazuh Detection) │
└──────────────┬───────────────┘
▼
┌──────────────────────────────┐
│ STEP 1: Create Case │
│ Severity: High | TLP: Amber │
└──────────────┬───────────────┘
▼
┌──────────────────────────────┐
│ STEP 2: Extract IOCs │
│ IP, Hash, URLs, Sender │
└──────────────┬───────────────┘
▼
┌──────────────────────────────┐
│ STEP 3: Reputation Check │
│ VirusTotal / AbuseIPDB │
└──────────┬─────────┬─────────┘
│ │
Malicious Clean
│ │
▼ ▼
┌──────────────┐ ┌──────────────┐
│ STEP 4: │ │ Close as │
│ Block IP │ │ False │
│ & Hash │ │ Positive │
└──────┬───────┘ └──────────────┘
▼
┌──────────────────────────────┐
│ STEP 5: Notify User │
│ Security awareness follow-up│
└──────────────┬───────────────┘
▼
┌──────────────────────────────┐
│ STEP 6: Close Case │
│ Resolution: True Positive │
└──────────────────────────────┘


### Playbook Summary (50 words)
*When a phishing alert is received, a case is created in TheHive with high severity. Indicators (IP, hash) are extracted and checked against threat intelligence. If confirmed malicious, the IP is blocked, the user is notified, and the case is documented. If clean, the alert is closed as false positive.*

---

## Case Documentation

### Case Details
| Field | Value |
|-------|-------|
| **Case ID** | #1 (-8413376) |
| **Title** | Phishing Alert: Suspicious Email from 203.0.113.50 |
| **Severity** | High |
| **TLP** | Amber |
| **Tags** | phishing, email, T1566 |
| **Created by** | analyst1@th.local |
| **Created at** | 28/04/2026 13:35 |
| **Closed at** | 28/04/2026 13:47 |
| **Time to Detect** | 2 minutes |
| **Time to Respond** | 14 minutes |
| **Resolution** | True Positive |

### Scenario Description
User reported receiving an external email with a suspicious PDF attachment. Subject: "Urgent Invoice Payment Required". Sender IP identified as 203.0.113.50. Attachment hash: d41d8cd98f00b204e9800998ecf8427e.

---

### Indicators of Compromise (IOCs)

| Type | Value | Tags | TLP |
|------|-------|------|-----|
| ip | 203.0.113.50 | phishing, C2 | Amber |
| hash | d41d8cd98f00b204e9800998ecf8427e | attachment, pdf | Amber |

---

### Playbook Tasks Executed

| # | Task | Status | Notes |
|---|------|--------|-------|
| 1 | Extract IOCs | ✅ Closed | Sender IP, attachment hash, and email subject extracted |
| 2 | Check IP Reputation | ✅ Closed | IP 203.0.113.50 verified as malicious (Known C2 infrastructure) |
| 3 | Check File Hash | ✅ Closed | Hash checked against threat intelligence |
| 4 | Block Indicators | ✅ Closed | IP 203.0.113.50 added to firewall/CrowdSec blocklist |
| 5 | Notify User | ✅ Closed | User notified via email with security awareness guidance |
| 6 | Close Case | ✅ Closed | Case documented and closed as True Positive |

---

## Response Timeline

| Timestamp | Action |
|-----------|--------|
| 13:33 | Case created (Detection time: 2 minutes from alert) |
| 13:35 | IOCs extracted and documented |
| 13:37 | IP reputation check initiated |
| 13:43 | Observables (IP, Hash) added to case |
| 13:44 | Block indicators task completed |
| 13:46 | User notification task completed |
| 13:47 | Case closed as True Positive |

**MTTD (Mean Time to Detect):** 2 minutes  
**MTTR (Mean Time to Respond):** 12 minutes (from detection to closure)

---

## Tools & Technologies Used

| Tool | Purpose |
|------|---------|
| **TheHive 5.2** | Case management, playbook execution, IOC tracking |
| **Docker** | Containerized deployment of TheHive + Cassandra |
| **MITRE ATT&CK** | Technique mapping (T1566 – Phishing) |

---

## Skills Demonstrated

- ✅ SOAR playbook design and execution
- ✅ Incident case management
- ✅ IOC extraction and documentation
- ✅ Role-based access control (analyst vs admin)
- ✅ MITRE ATT&CK technique mapping
- ✅ Metrics calculation (MTTD, MTTR)

---

## Observables (Screenshots)

| Screenshot | Description |
|------------|-------------|
| `case_creation.png` | TheHive case with title, severity, tags, and description |
| `tasks_list.png` | All 6 playbook tasks with completion status |
| `observables.png` | IP and Hash observables with tags |
| `case_closed.png` | Closed case showing True Positive resolution and timeline |

---

## Key Observations

1. **Role separation works correctly** — analyst1 can create cases but cannot modify organization settings (admin required)
2. **Task tracking** provides clear audit trail of all actions during response
3. **Observables** linked to the case enable future correlation with other incidents
4. **14-minute total handling time** demonstrates efficiency of structured playbook approach
5. **TLP Amber** marking ensures sensitive indicators are shared appropriately

---

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| TheHive initially not accessible on port 9000 | Restarted Docker containers with proper Cassandra dependency order |
| Understanding TheHive case structure | Referenced TheHive documentation for case, task, and observable hierarchy |
| Simulating real alert without full automation | Manually created case mimicking real Wazuh/SIEM alert payload |

---

## Real-World Application

In a production SOC environment, this playbook would be fully automated:
- **Wazuh** detects phishing via email gateway logs (rule ID triggers)
- **Webhook** sends alert JSON to TheHive API
- **TheHive** auto-creates case with IOCs pre-populated
- **Cortex** automatically runs analyzers (VirusTotal, AbuseIPDB) on observables
- **Responders** block the IP on the firewall without manual intervention
- **Analyst** only intervenes for complex investigations

This manual simulation demonstrates understanding of each step that would be automated in production.

---

## Lessons Learned

1. Structured playbooks drastically reduce response time (14 min vs unstructured hours)
2. IOC documentation in a central platform prevents duplication of effort
3. Role-based access (analyst vs admin) mirrors real SOC hierarchy
4. Tags (phishing, T1566, C2) enable quick filtering and trend analysis
5. TLP markings ensure proper information sharing boundaries

---

## Conclusion

The SOAR playbook development task was successfully completed. A phishing incident response playbook was designed and executed end-to-end in TheHive. The case was created with proper severity, all IOCs were documented, malicious indicators were blocked, affected user was notified, and the case was closed with a True Positive resolution. The complete workflow demonstrates proficiency in incident response automation and case management best practices.

---

**Status:** ✅ Complete  
**Date:** April 28, 2026  
**Analyst:** analyst1@th.local  
**Organization:** SOC

---

**Screenshot References:**
- `screenshots/case_creation.png` – Case creation with details
- `screenshots/tasks_progress.png` – Tasks execution in progress
- `screenshots/observables.png` – IOCs (IP + Hash) added
- `screenshots/case_closed.png` – Case closed as True Positive