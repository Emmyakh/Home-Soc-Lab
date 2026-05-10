# Home SOC Lab — Attack Simulation & Detection

A hands-on cybersecurity home lab built to simulate real-world attacks and 
detect them using industry-standard tools. This project demonstrates practical 
SOC analyst skills including threat detection, log analysis, SIEM operation, 
detection engineering, and incident response documentation.

## Lab Environment

| Component | Role | IP Address | OS / Tool |
|-----------|------|------------|-----------|
| Win10-Lab VM | Target / Victim | 192.168.10.10 | Windows 10 |
| Kali Linux VM | Attacker | 192.168.10.20 | Kali Linux |
| Host PC | SIEM | 172.20.10.3 | Splunk Enterprise |

## Tools Used

- VirtualBox — isolated lab network
- Sysmon v15.20 (SwiftOnSecurity config) — endpoint telemetry
- Splunk Enterprise 10.2 — SIEM and detection engineering
- Nmap 7.98 — network reconnaissance
- Hydra v9.6 — brute force credential attack
- Windows Event Viewer — log analysis

## Lab Structure

| Level | Topic | Key Outcome |
|-------|-------|-------------|
| 1 | Environment Setup | Isolated lab with Kali and Windows VMs |
| 2 | Reconnaissance & Detection | Nmap scan detected via Event ID 5156 |
| 3 | Credential Attacks | Hydra brute force detected via Event ID 4625 |
| 4 | SIEM | Splunk ingesting 24,376 events with attack dashboard |
| 5 | Detection Engineering | 3 custom Splunk alerts built and enabled |
| 6 | Incident Response | Full professional IR report produced |

## Key Skills Demonstrated

- Network reconnaissance detection
- Brute force attack simulation and detection
- Windows event log analysis (Event IDs 4625, 5156, 1, 3)
- Sysmon deployment and configuration
- Splunk SIEM setup, search, and dashboard creation
- Detection rule writing in Splunk SPL
- MITRE ATT&CK framework mapping
- Professional incident response documentation

## Incident Response Report

Full IR report available in the 
[Level-6-Incident-Response](./Level-6-Incident-Response/) folder.
