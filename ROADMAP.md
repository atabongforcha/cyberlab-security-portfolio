# CyberLab Project Roadmap

This roadmap organizes **50 hands-on cybersecurity projects** into six integrated portfolio categories. Together, these projects demonstrate capabilities across identity security, Windows security, detection engineering, offensive security, network architecture, vulnerability management, compliance, incident response, cloud security, DevSecOps, AI security, governance, and security architecture.

## Roadmap Summary

| Portfolio Category                            | Number of Projects |
| --------------------------------------------- | -----------------: |
| Identity, Windows & Detection Engineering     |                 13 |
| Offensive Security & Network Architecture     |                  7 |
| Vulnerability, Compliance & Incident Response |                  8 |
| AWS, Cloud & DevSecOps                        |                 10 |
| AI Security                                   |                  7 |
| Governance, Architecture & Capstone           |                  5 |
| **Total**                                     |             **50** |

## Status Legend

| Status         | Meaning                                        |
| -------------- | ---------------------------------------------- |
| ✅ Completed    | Implemented, tested, validated, and documented |
| 🚧 In Progress | Currently being developed                      |
| 🟡 Started     | Foundational work has begun                    |
| 🔴 Next        | Immediate recommended priority                 |
| 📋 Planned     | Scheduled for future implementation            |

---

## 1. Identity, Windows & Detection Engineering

Projects in this category demonstrate Active Directory administration, Windows security monitoring, centralized logging, SIEM engineering, authentication-attack detection, privileged-account monitoring, and endpoint visibility.

| No. | Project                                                      | Status      |
| --: | ------------------------------------------------------------ | ----------- |
|   1 | Active Directory Security & Domain Controller Administration | ✅ Completed |
|   2 | Windows Security Logging & Event Forwarding                  | ✅ Completed |
|   3 | Splunk SIEM Deployment & Detection Engineering               | ✅ Completed |
|   4 | Wazuh SIEM / Endpoint Monitoring                             | ✅ Completed |
|   5 | Failed Logon Detection                                       | ✅ Completed |
|   6 | Active Directory Account Lockout Detection                   | ✅ Completed |
|   7 | Password Spray Detection                                     | 🔴 Next     |
|   8 | Brute-Force Authentication Detection                         | 📋 Planned  |
|   9 | Successful Login After Failed Attempts                       | 📋 Planned  |
|  10 | Privileged Account Monitoring                                | 📋 Planned  |
|  11 | Active Directory Account Administration Monitoring           | ✅ Completed |
|  12 | PowerShell Security Monitoring                               | 📋 Planned  |
|  13 | Windows Persistence Detection                                | 📋 Planned  |

---

## 2. Offensive Security & Network Architecture

Projects in this category demonstrate controlled attack simulation, vulnerability discovery, reconnaissance detection, firewall administration, network segmentation, Zero Trust implementation, and DMZ architecture.

| No. | Project                                  | Status     |
| --: | ---------------------------------------- | ---------- |
|  14 | Kali Reconnaissance Detection            | 📋 Planned |
|  15 | Metasploitable2 Vulnerability Assessment | 🟡 Started |
|  16 | Controlled Exploitation Lab              | 📋 Planned |
|  17 | Network Attack Detection                 | 📋 Planned |
|  18 | Firewall / pfSense Security Architecture | 📋 Planned |
|  19 | Zero Trust Architecture Demonstration    | 📋 Planned |
|  20 | DMZ Architecture Project                 | 📋 Planned |

---

## 3. Vulnerability, Compliance & Incident Response

Projects in this category demonstrate vulnerability-management operations, security hardening, compliance assessment, detection development, threat hunting, incident response, MITRE ATT&CK mapping, and security automation.

| No. | Project                          | Status         |
| --: | -------------------------------- | -------------- |
|  21 | Vulnerability Management Program | 📋 Planned     |
|  22 | SCAP / STIG Compliance Hardening | 📋 Planned     |
|  23 | Incident Response Case Study     | 📋 Planned     |
|  24 | MITRE ATT&CK Mapping             | 📋 Planned     |
|  25 | Threat Hunting                   | 📋 Planned     |
|  26 | Detection Engineering Lifecycle  | 🚧 In Progress |
|  27 | Security Automation with Python  | 📋 Planned     |
|  28 | SOAR-Style Automation            | 📋 Planned     |

---

## 4. AWS, Cloud & DevSecOps

Projects in this category demonstrate AWS security, identity and access management, secure EC2 administration, cloud monitoring, misconfiguration detection, Infrastructure as Code, CI/CD security, container security, Kubernetes security, and multicloud architecture.

| No. | Project                          | Status         |
| --: | -------------------------------- | -------------- |
|  29 | AWS CyberLab Security            | 🚧 In Progress |
|  30 | AWS IAM Least-Privilege Project  | 🚧 In Progress |
|  31 | AWS Secure EC2 Administration    | ✅ Completed    |
|  32 | AWS Security Monitoring          | 🚧 In Progress |
|  33 | AWS Misconfiguration Detection   | 📋 Planned     |
|  34 | Infrastructure as Code Security  | 📋 Planned     |
|  35 | DevSecOps Pipeline               | 📋 Planned     |
|  36 | Container Security               | 📋 Planned     |
|  37 | Kubernetes Security              | 📋 Planned     |
|  38 | Cloud Multi-Environment Security | 📋 Planned     |

---

## 5. AI Security

Projects in this category demonstrate local AI security testing, prompt-injection assessment, sensitive-data protection, retrieval-augmented generation security, AI-agent security, AI red teaming, and AI governance.

| No. | Project                         | Status     |
| --: | ------------------------------- | ---------- |
|  39 | AI Security Lab                 | 🟡 Started |
|  40 | Prompt Injection Testing        | 📋 Planned |
|  41 | LLM Data Leakage Testing        | 📋 Planned |
|  42 | RAG Security                    | 📋 Planned |
|  43 | AI Agent Security               | 📋 Planned |
|  44 | AI Red Teaming                  | 📋 Planned |
|  45 | AI Governance & Risk Management | 📋 Planned |

---

## 6. Governance, Architecture & Capstone

Projects in this category demonstrate cybersecurity governance, NIST Risk Management Framework implementation, System Security Plan development, security architecture documentation, executive reporting, and end-to-end purple-team operations.

| No. | Project                             | Status         |
| --: | ----------------------------------- | -------------- |
|  46 | GRC / RMF Portfolio Project         | 📋 Planned     |
|  47 | System Security Plan (SSP) Project  | 📋 Planned     |
|  48 | Security Architecture Documentation | 🚧 In Progress |
|  49 | Executive Security Reporting        | 📋 Planned     |
|  50 | Full Purple-Team Capstone           | 📋 Planned     |

---

## Current Priority

The next recommended CyberLab project is **Password Spray Detection**.

This project will simulate controlled, low-and-slow authentication attempts against multiple test accounts. Splunk detection logic will be developed to identify one source attempting authentication across several accounts within a defined period.

The project will include:

* Controlled password-spray simulation
* Windows authentication-event collection
* Splunk correlation and threshold logic
* Detection validation and tuning
* False-positive considerations
* Incident investigation
* MITRE ATT&CK mapping
* Remediation recommendations
* Screenshots and portfolio evidence
* GitHub case-study documentation

## Project Documentation Standard

Each completed project should contain the following portfolio evidence:

1. Project overview
2. Security objectives
3. Lab architecture
4. Technologies and tools used
5. Implementation procedure
6. Detection queries or security controls
7. Test or attack simulation
8. Investigation findings
9. Screenshots and supporting evidence
10. Remediation actions
11. Lessons learned
12. MITRE ATT&CK mapping, when applicable
13. Resume-ready achievement statement

## Portfolio Objective

The CyberLab provides verifiable evidence of practical cybersecurity experience across enterprise, cloud, hybrid, offensive, defensive, governance, and emerging AI-security environments.

The completed projects demonstrate the ability to design security controls, administer security technologies, simulate threats, engineer detections, investigate alerts, remediate vulnerabilities, document findings, and communicate technical risks to both technical and executive audiences.
