# Level 4 — SIEM Setup & Investigation (Splunk)

## Objective
Deploy Splunk as a centralised SIEM, ingest Windows Security and 
Sysmon logs from the target VM, and build a dashboard visualising 
the attacks from Levels 2 and 3.

## Setup

- Splunk Enterprise 10.2 installed on host PC
- Windows Security logs exported as SecurityLogs.evtx
- Sysmon logs exported as SysmonLogs.evtx
- Both uploaded to Splunk via Settings → Add Data → Upload

## Log Sources Ingested

| Source | Event Count |
|--------|-------------|
| WinEventLog:Security | 12,758 |
| WinEventLog:Microsoft-Windows-Sysmon/Operational | 11,618 |
| **Total** | **24,376** |

## Key Splunk Searches

**All events by source:**
index=main | stats count by sourcetype

**Brute force detection:**
index=main EventCode=4625
| stats count by Account_Name, Source_Network_Address

**Port scan detection:**
index=main EventCode=5156
| stats count by Source_Address, Destination_Port
| sort -count | head 20

## Dashboard Built

**Name:** SOC LAB - Attack Detection  
**Panels:**
1. Failed Logon Attempts — Brute Force Attack (table)
2. Network Scan Detection — Nmap (table)
3. Total Security Events (single value)

## Key Findings in Splunk

- 192.168.10.20 (Kali) made 13 failed logon attempts against testuser
- 192.168.10.20 connected to port 3389 (RDP) 46 times
- 192.168.10.20 connected to port 445 (SMB) 31 times
- 2,376 Windows Filtering Platform events from the Nmap scan

## Screenshots

See `/screenshots/` folder for evidence.
