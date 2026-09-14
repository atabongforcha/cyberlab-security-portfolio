# CyberLab Security Portfolio

Hands-on cybersecurity lab demonstrating enterprise security architecture, Active Directory security, SIEM monitoring, detection engineering, attack simulation, incident investigation, and remediation.
## Project Roadmap

This CyberLab contains **50 hands-on cybersecurity projects** organized across six integrated portfolio categories.

[View the complete CyberLab Project Roadmap](ROADMAP.md)

## Lab Environment

- VMware Workstation
- Windows Server 2025
- Active Directory Domain Services (AD DS)
- Windows 11 Enterprise
- Splunk Enterprise
- Wazuh
- Kali Linux
- Metasploitable2
- Ubuntu Linux
- AI Security VM

## Security Capabilities Demonstrated

- Active Directory administration and security monitoring
- Windows Security Event analysis
- SIEM deployment and configuration
- Splunk detection engineering
- Authentication attack detection
- Event correlation
- Threat investigation
- Incident response and remediation
- Vulnerability assessment
- Network reconnaissance
- Security automation

## Detection & Investigation Exercises

### 1. Failed Logon Detection
Detection and investigation of Windows failed authentication events using Splunk.

### 2. Active Directory Account Lockout Detection
Correlated repeated Kerberos authentication failures (Event ID 4771) with Active Directory account lockouts (Event ID 4740).

### 2. Active Directory Account Lockout Detection
Correlated repeated Kerberos authentication failures (Event ID 4771) with Active Directory account lockouts (Event ID 4740).

### 3. [Windows Active Directory Password Spray Detection with Splunk](10-password-spray-detection/)
Simulated a controlled password spray against six Active Directory test accounts, detected Windows Security Event ID 4625 activity using Splunk XML field extraction and SPL correlation, and operationalized a scheduled high-severity alert.

### Upcoming Exercises
- Network Reconnaissance Detection
- Vulnerable Service Investigation
- PowerShell Activity Detection
- Incident Response & Remediation
