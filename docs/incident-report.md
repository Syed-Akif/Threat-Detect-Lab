# Incident Report: SSH Brute-Force Attack Detection

## 1. Executive Summary
A series of SSH authentication failures were detected on a Linux endpoint monitored by Wazuh SIEM.  
The activity originated from an internal attacker machine and was identified as a brute-force password guessing attempt.  
The incident was detected, analyzed, and correlated using Wazuh security rules and MITRE ATT&CK mapping.

---

## 2. Environment Overview
- SIEM Platform: Wazuh
- Endpoint OS: Ubuntu Linux
- Attacker OS: Kali Linux
- Network Type: Internal Virtual Lab
- Log Source: /var/log/auth.log

---

## 3. Attack Description
An attacker attempted multiple SSH login attempts against the Linux endpoint using a password list.  
The attack generated repeated authentication failures within a short time window, triggering Wazuh correlation rules.

---

## 4. Detection Details
- Detection Tool: Wazuh SIEM
- Rule IDs:
  - 5503 – PAM User login failed
  - 5760 – SSH authentication failed
  - 5551 – Multiple failed logins detected
- Alert Severity:
  - Level 5 (Authentication failure)
  - Level 10 (Brute-force correlation)

---

## 5. MITRE ATT&CK Mapping
- Tactic: Credential Access
- Techniques:
  - T1110.001 – Password Guessing
  - T1021.004 – Remote Services (SSH)

---

## 6. Impact Assessment
- No successful unauthorized access was confirmed.
- No privilege escalation observed.
- Attack was limited to authentication attempts only.

---

## 7. Response & Recommendations
- Block the attacking IP address.
- Enforce SSH hardening (disable root login, key-based authentication).
- Implement rate limiting or fail2ban.
- Continue monitoring authentication logs.

---

## 8. Conclusion
This incident demonstrates the effectiveness of Wazuh SIEM in detecting, correlating, and analyzing brute-force attacks on Linux systems.  
The alert lifecycle from detection to investigation reflects real SOC monitoring operations.
