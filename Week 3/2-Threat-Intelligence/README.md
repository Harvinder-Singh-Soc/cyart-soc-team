# Threat Intelligence Integration

**Environment:** Wazuh Server (192.168.56.100)  
**Data Source:** Windows Endpoint Agent (192.168.56.150)  
**Date:** 29 April 2026

---

## 1. Threat Feed Import — AlienVault OTX

Configured AlienVault OTX integration in Wazuh to automatically import threat intelligence feeds.

**Configuration File:** `/var/ossec/etc/ossec.conf`

```xml
<integration>
  <name>alienvault</name>
  <api_key>ef356e99e33895270b8592e43df9ab8175633d1e82415fa700884046a8dfc89</api_key>
  <group>syscheck</group>
  <alert_format>json</alert_format>
</integration>

Imported OTX pulses automatically match IOCs against incoming logs.

https://screenshots/wazuh-otx-integration.png

2. Alert Enrichment

Wazuh automatically enriches alerts with MITRE ATT&CK mappings, compliance standards, and threat context.

Expanded Alert — Event ID 4624 (Successful Logon):

screenshots/enriched-alert_1.png

screenshots/enriched-alert_2.png

Enrichment Table:
Alert ID	IP	User	Logon Type	MITRE Technique	Fired Times
60118	192.168.56.150	Harvinder Singh	2 (Interactive)	T1078 - Valid Accounts	8

Additional Enrichment Fields:

    rule.mitre.tactic: Defense Evasion, Persistence, Privilege Escalation, Initial Access

    rule.groups: windows, windows_security, authentication_success

    Compliance: PCI DSS (10.2.5), HIPAA (164.312.b), GDPR (IV_32.2), NIST 800-53 (AU.14, AC.9)

    decoder: windows_eventchannel

    rule.level: 3

3. Threat Hunting — T1078 (Valid Accounts)

Proactively hunted for Valid Accounts misuse using Wazuh Discover.

Query Used:

data.win.system.eventID: 4624 AND data.win.eventData.targetUserName: *

Results: 8 hits from Windows-Endpoint within the search window

Findings: All logons mapped to user "Harvinder Singh" via Logon Type 2 (Interactive). No unusual off-hours activity or unauthorized account usage detected. Query saved for continuous monitoring.

screenshots/threat-hunting.png

MITRE ATT&CK Mapping:

    Technique: T1078 — Valid Accounts

    Tactics: Defense Evasion, Persistence, Privilege Escalation, Initial Access

    Detection: Monitor Event ID 4624 for unusual accounts, off-hours logins, or anomalous logon types

Tools Used

    Wazuh 4.x — SIEM & Threat Detection

    AlienVault OTX — Threat Intelligence Feeds

    Windows Security Events — Log Source

    MITRE ATT&CK — Threat Classification

    Skills Applied: Threat feed integration, IOC enrichment, alert triage with MITRE mapping, proactive threat hunting


## 📁 Folder Structure:

2-Threat-Intelligence/
├── README.md
└── screenshots/
├── wazuh-otx-integration.png
├── enriched-alert_1.png
├── enriched-alert_2.png
└── threat-hunting.png
