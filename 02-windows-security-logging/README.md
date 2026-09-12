# Windows Security Logging & Event Forwarding

## Project Overview

This project demonstrates the configuration and validation of advanced Windows security auditing, Windows Remote Management (WinRM), Windows Event Forwarding (WEF), and centralized event collection in a Windows Active Directory CyberLab.

Security events generated on the Windows 11 Enterprise endpoint were collected centrally to improve visibility into authentication activity, account changes, PowerShell execution, policy changes, and other security-relevant behavior.

## Project Status

✅ Completed

## Project Objectives

* Configure advanced Windows security auditing
* Enable security-event collection across domain systems
* Configure Windows Remote Management
* Implement Windows Event Forwarding
* Centralize Windows events for investigation
* Validate the collection of authentication and security events
* Improve visibility into endpoint and identity activity
* Prepare Windows events for analysis in Splunk Enterprise and Wazuh
* Document the implementation with sanitized evidence

## Lab Environment

| Component               | Configuration                            |
| ----------------------- | ---------------------------------------- |
| Hypervisor              | VMware Workstation                       |
| Domain Controller       | Windows Server 2025 — `DC01`             |
| Active Directory Domain | `cyberlab.local`                         |
| Source Endpoint         | Windows 11 Enterprise — `WIN11-CLIENT01` |
| Audit Configuration     | Advanced Audit Policy                    |
| Remote Management       | Windows Remote Management                |
| Event Collection        | Windows Event Forwarding                 |
| Central Event Log       | Forwarded Events                         |
| Local Validation        | Windows Event Viewer and PowerShell      |
| Security Monitoring     | Splunk Enterprise and Wazuh              |

## Architecture

The logging architecture consists of:

* `WIN11-CLIENT01` generating Windows security events
* Advanced Audit Policy controlling which events are recorded
* WinRM supporting remote management and event-forwarding communication
* Windows Event Forwarding transmitting selected events
* A centralized Windows event collector receiving forwarded events
* Windows Event Viewer providing local validation
* Splunk Enterprise and Wazuh providing additional monitoring and analysis

## Implementation

### 1. Advanced Audit Policy Configuration

Configured advanced Windows auditing to record security-relevant activity across the domain environment.

Audit categories included:

* Account logon
* Account management
* Detailed tracking
* Logon and logoff
* Policy change
* Privilege use
* System activity
* PowerShell activity

The audit configuration improved visibility into authentication behavior, identity changes, administrative activity, and security-policy events.

### 2. Authentication Auditing

Configured logging for successful and failed authentication activity.

Relevant events included:

| Event ID | Description                                |
| -------: | ------------------------------------------ |
|     4624 | Successful account logon                   |
|     4625 | Failed account logon                       |
|     4634 | Account logoff                             |
|     4648 | Logon using explicit credentials           |
|     4672 | Special privileges assigned to a new logon |
|     4740 | User account locked out                    |

These events support failed-logon detection, account-lockout investigation, privileged-session monitoring, and authentication analysis.

### 3. Account-Management Auditing

Configured auditing to provide visibility into changes involving users, groups, and other Active Directory objects.

Relevant events included:

| Event ID | Description                                 |
| -------: | ------------------------------------------- |
|     4720 | User account created                        |
|     4722 | User account enabled                        |
|     4723 | Attempt to change an account password       |
|     4724 | Attempt to reset an account password        |
|     4725 | User account disabled                       |
|     4726 | User account deleted                        |
|     4728 | Member added to a global security group     |
|     4729 | Member removed from a global security group |
|     4732 | Member added to a local security group      |
|     4733 | Member removed from a local security group  |
|     4738 | User account changed                        |

These events help identify unauthorized identity changes and support privileged-account monitoring.

### 4. PowerShell Logging

Configured PowerShell logging to improve visibility into command execution and administrative activity.

Relevant events included:

| Event ID | Description                     |
| -------: | ------------------------------- |
|      400 | PowerShell engine started       |
|      403 | PowerShell engine stopped       |
|      600 | PowerShell provider activity    |
|     4103 | PowerShell module logging       |
|     4104 | PowerShell script-block logging |

PowerShell auditing supports the investigation of legitimate administration, suspicious scripts, and command-based attack activity.

### 5. Windows Remote Management

Configured Windows Remote Management to support communication between the event source and collector.

Validation included:

* Confirming that the WinRM service was available
* Verifying that the service was configured correctly
* Confirming connectivity between the source endpoint and collector
* Reviewing the Windows Remote Management configuration
* Verifying that domain policies supported the required communication

### 6. Windows Event Collector

Configured the Windows Event Collector service to receive forwarded Windows events.

Implementation activities included:

* Enabling the Windows Event Collector service
* Configuring the event collector
* Creating an event subscription
* Identifying the source computer
* Selecting the required event channels
* Confirming that the subscription was active
* Reviewing collected events in the Forwarded Events log

### 7. Windows Event Forwarding

Configured Windows Event Forwarding to send selected security events from the source endpoint to the centralized collector.

The forwarding configuration supported collection of:

* Successful logons
* Failed logons
* Account lockouts
* Account-management changes
* Privileged logons
* PowerShell activity
* Other security-relevant Windows events

### 8. Group Policy Configuration

Used Group Policy to apply consistent audit and event-forwarding settings to domain systems.

Policy areas included:

* Advanced Audit Policy Configuration
* Windows Remote Management
* Event Forwarding
* PowerShell logging
* Security log configuration
* Windows Firewall rules required for authorized communication

Group Policy provided centralized and repeatable configuration across the lab environment.

### 9. Centralized Event Collection

Validated that events generated on the Windows 11 endpoint appeared in the centralized Forwarded Events log.

Centralized collection improved the ability to:

* Review endpoint activity from one location
* Correlate authentication events
* Investigate account lockouts
* Detect suspicious administrative changes
* Preserve security-event visibility
* Forward relevant events to SIEM and endpoint-monitoring platforms

## Validation Activities

### Audit Policy Validation

The effective audit policy was reviewed to confirm that the required audit categories were enabled.

Command used:

`auditpol /get /category:*`

Validation confirmed that the required security-auditing categories were active.

### Group Policy Validation

The following commands were used to refresh and verify Group Policy:

* `gpupdate /force`
* `gpresult /r`
* `gpresult /h C:\Temp\gpresult.html`

The results were reviewed to confirm that the expected logging and event-forwarding policies were applied.

### WinRM Validation

WinRM configuration and service availability were reviewed using:

* `winrm quickconfig`
* `winrm get winrm/config`
* `Get-Service WinRM`

Validation confirmed that Windows Remote Management was available for authorized event-forwarding communication.

### Event Collector Validation

The Windows Event Collector service and subscriptions were reviewed using:

* `Get-Service Wecsvc`
* `wecutil enum-subscription`
* `wecutil get-subscription <SubscriptionName>`

The results confirmed that the event-collection service and subscription were available.

### Forwarded Events Validation

Forwarded events were reviewed through:

* Event Viewer
* Applications and Services Logs
* Forwarded Events
* PowerShell event-log queries

Example validation command:

`Get-WinEvent -LogName ForwardedEvents -MaxEvents 20`

The results confirmed that security events generated on the source endpoint were received by the centralized collector.

### Authentication Event Validation

Controlled authentication activity was generated and reviewed to confirm the presence of:

* Event ID `4624` for successful authentication
* Event ID `4625` for failed authentication
* Event ID `4740` for account-lockout activity

### PowerShell Event Validation

PowerShell activity was generated in the lab and reviewed to verify the presence of relevant PowerShell events, including event IDs `4103` and `4104`.

## Tools and Technologies Used

| Tool or Technology               | Purpose                                                           |
| -------------------------------- | ----------------------------------------------------------------- |
| VMware Workstation               | Hosted the virtual CyberLab systems                               |
| Windows Server 2025              | Hosted the domain services and centralized Windows administration |
| Windows 11 Enterprise            | Generated endpoint security events                                |
| Active Directory Domain Services | Provided centralized identity and domain management               |
| Group Policy Management          | Applied audit and event-forwarding configurations                 |
| Advanced Audit Policy            | Controlled security-event generation                              |
| Windows Remote Management        | Supported authorized remote communication                         |
| Windows Event Forwarding         | Forwarded selected events to the collector                        |
| Windows Event Collector          | Received and stored forwarded events                              |
| Windows Event Viewer             | Reviewed local and forwarded events                               |
| PowerShell                       | Supported configuration, validation, and event review             |
| `auditpol`                       | Displayed effective audit-policy settings                         |
| `gpupdate`                       | Refreshed Group Policy                                            |
| `gpresult`                       | Verified applied Group Policies                                   |
| `wecutil`                        | Managed and validated event subscriptions                         |
| Splunk Enterprise                | Supported centralized event analysis and detection                |
| Wazuh                            | Supported endpoint monitoring and event visibility                |

## Security Skills Demonstrated

* Windows security logging
* Advanced Audit Policy configuration
* Windows Event Forwarding
* Windows Event Collector administration
* Windows Remote Management
* Centralized security-event collection
* Active Directory security monitoring
* Authentication-event analysis
* Account-management monitoring
* Account-lockout investigation
* PowerShell security logging
* Group Policy administration
* Windows Event Viewer analysis
* SIEM data-source preparation
* Endpoint-monitoring integration
* Event validation and troubleshooting
* Security evidence documentation

## Project Results

The project established centralized Windows security logging within the CyberLab and achieved the following results:

* Advanced Windows auditing was configured
* Authentication and account-management events were generated and reviewed
* PowerShell logging improved visibility into command execution
* WinRM supported authorized communication between domain systems
* Windows Event Forwarding transmitted selected security events
* The Windows Event Collector received endpoint events
* Forwarded events were validated in the centralized event log
* Security events were prepared for Splunk Enterprise and Wazuh analysis
* Centralized logging supported later detection and investigation projects

This project provides the logging foundation for failed-logon detection, account-lockout correlation, password-spray detection, privileged-account monitoring, threat hunting, and incident response.

## Evidence

The following sanitized evidence should support the project:

### Advanced Audit Policy

* Effective audit-policy configuration
* Enabled logon, account-management, policy-change, and detailed-tracking categories
* Output from `auditpol /get /category:*`

### Group Policy

* Advanced Audit Policy Group Policy settings
* WinRM policy configuration
* Event-forwarding subscription-manager configuration
* Successful `gpupdate` and `gpresult` validation

### Windows Remote Management

* WinRM service status
* WinRM configuration or connectivity validation

### Windows Event Collector

* Windows Event Collector service running
* Configured event subscription
* Active subscription status

### Forwarded Events

* Events displayed in the Forwarded Events log
* Sanitized source-computer information
* Relevant authentication or account-management event details

### Authentication Events

* Event ID `4624` showing a successful logon
* Event ID `4625` showing a failed logon
* Event ID `4740` showing an account lockout

### PowerShell Events

* Event ID `4103` or `4104` displayed in Event Viewer
* Sanitized PowerShell activity used for validation

> **Evidence notice:** Passwords, IP addresses, personal information, account identifiers, and unnecessary system or resource identifiers must be removed or obscured before screenshots are published.

## Challenges and Resolutions

### Event-Forwarding Connectivity

**Challenge:** Event forwarding depended on working network connectivity, DNS resolution, WinRM, firewall rules, and domain authentication.

**Resolution:** Verified connectivity and DNS, confirmed the WinRM service status, reviewed the applicable policies, and validated authorized communication between the source endpoint and collector.

### Group Policy Application

**Challenge:** Newly configured auditing and forwarding policies were not always visible immediately.

**Resolution:** Used `gpupdate /force` to refresh policies and `gpresult` to verify that the correct Group Policy Objects were applied.

### Missing Forwarded Events

**Challenge:** Events did not appear until the source configuration, collector service, subscription, and event selection were correctly aligned.

**Resolution:** Verified the Windows Event Collector service, reviewed the subscription configuration, generated controlled test activity, and checked the Forwarded Events log again.

### Event Volume

**Challenge:** Collecting too many Windows events can increase noise and make investigations less efficient.

**Resolution:** Focused collection on security-relevant authentication, account-management, privilege, policy-change, and PowerShell events.

### Security and Privacy

**Challenge:** Event details and screenshots can expose usernames, IP addresses, computer names, and other identifiers.

**Resolution:** Reviewed and sanitized evidence before publishing it in the public GitHub portfolio.

## Lessons Learned

* Windows logging must be configured intentionally because default auditing may not provide sufficient investigative detail.
* Centralized event collection improves visibility across multiple systems.
* Active Directory, DNS, Group Policy, WinRM, firewall settings, and WEF must operate together.
* Audit policies should align with specific detection and investigation objectives.
* Authentication events provide essential context for failed-logon and account-lockout investigations.
* PowerShell logging improves visibility into administrative and potentially malicious activity.
* Group Policy provides consistent and scalable logging configuration.
* Controlled test activity is necessary to validate event generation and forwarding.
* Effective security monitoring requires both event collection and meaningful analysis.
* Public evidence must be sanitized before publication.

## Security and Privacy Statement

* All systems and security events were created in an isolated and authorized CyberLab environment.
* No production systems or third-party accounts were accessed.
* Test activity was performed only against systems owned and controlled within the lab.
* Sensitive information is removed or obscured before evidence is published.

## Related CyberLab Projects

* Active Directory Security and Domain Controller Administration
* Splunk SIEM Deployment and Detection Engineering
* Wazuh SIEM and Endpoint Monitoring
* Failed Logon Detection
* Account Lockout Detection
* Password Spray Detection
* Privileged Account Monitoring
