# Level 5 — Detection Engineering

## Objective
Write custom Splunk detection rules that automatically alert on 
attack patterns identified in Levels 2 and 3.

## Alerts Created

### Alert 1 — Brute Force Attack Detected
**SPL Query:**
index=main EventCode=4625
| stats count by Source_Network_Address
| where count > 5

**Logic:** Any IP generating more than 5 failed logon events  
**Schedule:** Runs every hour  
**Status:** Enabled

---

### Alert 2 — Port Scan Detected
**SPL Query:**
index=main EventCode=5156
| stats dc(Destination_Port) as unique_ports by Source_Address
| where unique_ports > 10

**Logic:** Any IP connecting to more than 10 unique ports  
**Schedule:** Runs every hour  
**Status:** Enabled

---

### Alert 3 — Suspicious Process Creation Detected
**SPL Query:**
index=main sourcetype="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1

**Logic:** Any Sysmon process creation event  
**Schedule:** Runs every hour  
**Status:** Enabled

## Key Learning

Alert thresholds must be carefully tuned:
- Too low = false positives overwhelming the SOC
- Too high = real attacks missed
- Threshold of 5 failed logons balances sensitivity and specificity

## MITRE ATT&CK Coverage

| Alert | Tactic | Technique |
|-------|--------|-----------|
| Brute Force | Credential Access | T1110.001 |
| Port Scan | Discovery | T1046 |
| Process Creation | Execution | T1059 |

## Screenshots

See `/screenshots/` folder for evidence.
