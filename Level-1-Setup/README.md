# Level 1 — Environment Setup

## Objective
Build an isolated attack and defence lab environment using VirtualBox.

## What Was Built

- Windows 10 VM (target machine) — IP: 192.168.10.10
- Kali Linux VM (attacker machine) — IP: 192.168.10.20
- Both VMs connected on an isolated VirtualBox internal network
- Sysmon v15.20 installed on Windows VM
- SwiftOnSecurity Sysmon config applied for comprehensive telemetry
- VirtualBox Guest Additions installed for file transfer between VMs

## Tools Installed

- Sysmon v15.20 with SwiftOnSecurity configuration
- VirtualBox Guest Additions
- Nmap (pre-installed on Kali)
- Hydra (pre-installed on Kali)

## Key Configuration

- Network type: VirtualBox Internal Network (isolated — no internet access)
- Sysmon config: SwiftOnSecurity sysmonconfig-export.xml
- Windows Filtering Platform auditing enabled via auditpol

## Outcome

Fully isolated lab environment with endpoint telemetry running, 
ready for attack simulation and detection exercises.
