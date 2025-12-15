# Attack Flow – SSH Brute Force Detection Lab

## Step 1: Environment Setup
- Wazuh SIEM deployed
- Ubuntu endpoint onboarded with Wazuh agent
- Kali Linux prepared as attacker

## Step 2: Attack Execution
- SSH brute-force attack launched from Kali using Hydra
- Multiple authentication attempts sent to the Ubuntu endpoint

## Step 3: Log Generation
- SSH authentication failures logged in /var/log/auth.log
- Logs forwarded to Wazuh manager via agent

## Step 4: Detection & Correlation
- Wazuh detected repeated login failures
- Alerts correlated into brute-force activity
- MITRE ATT&CK techniques mapped automatically

## Step 5: Analysis
- Alerts reviewed in Wazuh dashboard
- Source IP, target user, and rule severity identified
