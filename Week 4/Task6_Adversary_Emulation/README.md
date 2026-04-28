# Task 6: Adversary Emulation

**Status:** Complete | **Date:** April 28, 2026

## Objective
Simulate adversary TTPs using MITRE Caldera and validate detection via Elastic Security.

## Tools
- Caldera (192.168.56.130:8888)
- Sandcat Agent on Windows Endpoint
- Elastic Security (Kibana)

## Emulation
- Adversary: Discovery
- Techniques: 7
- Successful: 6
- Failed: 1 (DC Discovery — expected)

## Detection
- Event ID: 4688 (Process Creation)
- Events Captured: 11
- SIEM: Elastic Stack

## MITRE ATT&CK
TA0007 — Discovery

## Screenshots
- agent_alive.png
- operation_running.png
- operation_completed.png
- elastic_detection.png