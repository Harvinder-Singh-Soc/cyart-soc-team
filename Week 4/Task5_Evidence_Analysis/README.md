# Task 5: Evidence Analysis

**Status:** Complete | **Date:** April 28, 2026

## Objective
Collect and analyze forensic evidence from Windows Endpoint using Velociraptor with proper chain of custody documentation.

## Tools
- Velociraptor (192.168.56.110:8889)
- Windows Endpoint (192.168.56.150)
- Google Sheets

## Method
- Query: `SELECT * FROM netstat()`
- Records collected: 77
- Chain of custody documented with SHA256 hash

## Findings
- Port 135 (RPC) - LISTEN
- Port 139 (NetBIOS) - LISTEN on multiple interfaces
- Standard Windows services, no immediate anomalies

## Screenshots
- velociraptor_collection.png
- netstat_data.png
- chain_of_custody.png