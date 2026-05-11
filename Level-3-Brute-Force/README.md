# Level 3 — Credential Brute Force Attack & Detection

## Objective
Simulate a brute force credential attack against the Windows VM 
and detect it using Windows Security event logs.

## Attack Performed

**Tool:** Hydra v9.6  
**Wordlist:** rockyou.txt (14,344,399 passwords)  
**Target:** testuser account via RDP (port 3389)  
**Source:** Kali Linux (192.168.10.20)  
**Command:** `hydra rdp://192.168.10.10 -l testuser -P /usr/share/wordlists/rockyou.txt -t 4 -W 3`

## Attack Result

| Metric | Value |
|--------|-------|
| Target account | testuser |
| Failed logon events | 16 x Event ID 4625 in 17 seconds |
| Password cracked | Yes — Password: 123456 |
| Attack duration | ~58 seconds |

## Detection Method

**Event ID:** 4625 — An account failed to log on  
**Log source:** Windows Security Event Log  
**Detection indicator:** 16 failed logon attempts from single IP in 17 seconds

## Splunk Detection Query
index=main EventCode=4625
| stats count by Account_Name, Source_Network_Address

## Result in Splunk

| Account | Source IP | Count |
|---------|-----------|-------|
| testuser | 192.168.10.20 | 13 |
| — | 192.168.10.20 | 13 |

## MITRE ATT&CK

- **Tactic:** Credential Access
- **Technique:** T1110 — Brute Force
- **Sub-technique:** T1110.001 — Password Guessing

## Recommended Response

- Lock testuser account immediately
- Block 192.168.10.20 at firewall
- Implement account lockout after 5 failed attempts
- Enforce MFA on all remote access
- Enforce strong password policy (minimum 14 characters)

## Screenshots

See `screenshots` folder for evidence.
