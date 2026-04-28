# Task 3: Post-Incident Analysis

## Objective
Root Cause Analysis, Fishbone Diagram, and Metrics Calculation for the phishing incident from Task 2.

## Incident Reference
- Case ID: #1
- Title: Phishing Alert: Suspicious Email from 203.0.113.50
- Resolution: True Positive
- Analyst: analyst1@th.local
- Date: April 28, 2026

## 5 Whys Analysis
| # | Question | Answer |
|---|----------|--------|
| 1 | Why did the phishing email reach the user? | Email filter did not catch the malicious message |
| 2 | Why did the email filter miss it? | Sender domain was newly registered |
| 3 | Why was a new domain allowed? | Default policy allows all domains |
| 4 | Why is the policy so permissive? | Security team not involved in setup |
| 5 | Why wasn't security involved? | No formal review process exists |

**Root Cause:** Lack of security review for email gateway configuration.

## Fishbone Categories
- People: User clicked link, lack of awareness
- Process: No security review for IT changes
- Technology: Permissive filter, no advanced detection
- Policy: No DMARC, no reporting process

## Metrics
| Metric | Value |
|--------|-------|
| MTTD | 2 minutes |
| MTTR | 12 minutes |
| Total | 14 minutes |

## Recommendations
- Default-deny email policy
- Security sign-off for IT changes
- Enable DMARC
- Quarterly phishing training

## Screenshots
- 5_whys_analysis.png
- fishbone_diagram.png
- metrics_calculation.png

**Status:** Complete