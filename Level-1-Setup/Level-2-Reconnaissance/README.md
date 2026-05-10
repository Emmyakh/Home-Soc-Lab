# Level 2 — Reconnaissance & Detection

## Objective
Simulate a network reconnaissance attack from Kali Linux and detect 
it on the Windows target using Sysmon and Windows Security logs.

## Attack Performed

**Tool:** Nmap 7.98  
**Command:** `nmap -sV 192.168.10.10`  
**Source:** Kali Linux (192.168.10.20)  
**Target:** Windows VM (192.168.10.10)

## Open Ports Discovered by Attacker

| Port | Service | Risk |
|------|---------|------|
| 135/TCP | Microsoft RPC | Lateral movement risk |
| 139/TCP | NetBIOS-SSN | Credential capture risk |
| 445/TCP | SMB | High — ransomware, EternalBlue |

## Detection Method

**Expected:** Sysmon Event ID 3 (Network Connection)  
**Actual:** Windows Security Event ID 5156 (WFP Connection Permitted)

### Key Finding
Sysmon Event ID 3 only logs **outbound** connections initiated by 
Windows processes. Nmap probes arrive at the network stack level 
before any Windows process owns the connection — so Sysmon does 
not log inbound scans.

The correct detection point is the **Windows Filtering Platform** 
(Event ID 5156), enabled via: auditpol /set /subcategory:"Filtering Platform Connection" /success:enable /failure:enable

## Evidence

- 2,376 Event ID 5156 entries generated in an 18-second window
- All from source IP 192.168.10.20 (Kali)
- Burst pattern clearly visible in Splunk timeline

## Splunk Detection Query
index=main EventCode=5156
| stats count by Source_Address, Destination_Port
| sort -count

## MITRE ATT&CK

- **Tactic:** Reconnaissance / Discovery
- **Technique:** T1046 — Network Service Discovery

## Screenshots

See `/screenshots/` folder for evidence.
