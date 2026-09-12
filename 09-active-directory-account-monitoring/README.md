# Active Directory Account Administration Monitoring

## Project Overview

This project demonstrates the monitoring and validation of critical Active Directory user-account administration events using Windows Security logs and Splunk Enterprise.

A Splunk dashboard was developed to provide centralized visibility into user-account creation, enablement, password-reset attempts, and account disablement. The project helps security analysts identify and investigate authorized, unexpected, or potentially malicious identity-administration activity.

## Project Status

✅ Completed

## Detection Summary

| Attribute           | Details                                            |
| ------------------- | -------------------------------------------------- |
| Security Use Case   | Active Directory account-administration monitoring |
| Primary Data Source | Windows Security logs                              |
| Splunk Sourcetype   | `XmlWinEventLog:Security`                          |
| Event Source        | Active Directory domain controller                 |
| Domain Controller   | `DC01`                                             |
| Analysis Platform   | Splunk Enterprise                                  |
| Visualization       | Splunk security dashboard                          |
| Security Domain     | Identity and Access Management                     |
| Status              | Completed and validated                            |

## Monitored Events

| Event ID | Description                                      | Security Significance                              |
| -------: | ------------------------------------------------ | -------------------------------------------------- |
|     4720 | A user account was created                       | Detects creation of new domain identities          |
|     4722 | A user account was enabled                       | Identifies accounts returned to an active state    |
|     4724 | An attempt was made to reset an account password | Detects administrative password-reset activity     |
|     4725 | A user account was disabled                      | Identifies removal or suspension of account access |

## Project Objectives

* Monitor Active Directory user-account administration
* Ingest domain-controller security events into Splunk
* Detect user-account creation
* Detect account enablement
* Detect administrative password-reset attempts
* Detect account disablement
* Create an analyst-readable Splunk dashboard
* Validate the dashboard with Windows Security events
* Support investigation of unauthorized identity changes
* Document the project with sanitized evidence

## Lab Environment

| Component                           | Purpose                                                             |
| ----------------------------------- | ------------------------------------------------------------------- |
| VMware Workstation                  | Hosted the virtual CyberLab systems                                 |
| Windows Server 2025 — `DC01`        | Hosted Active Directory and generated account-administration events |
| Active Directory — `cyberlab.local` | Provided centralized identity administration                        |
| Windows Security Log                | Recorded account-management activity                                |
| Windows Event Forwarding            | Supported centralized Windows event collection                      |
| Splunk Forwarder                    | Sent Windows Security events to Splunk                              |
| Splunk Enterprise                   | Searched, analyzed, and visualized account activity                 |
| SPL                                 | Filtered and summarized account-administration events               |
| Windows Event Viewer                | Validated original Windows events                                   |
| Wazuh                               | Provided complementary endpoint-event visibility                    |

## Monitoring Architecture

The completed monitoring workflow consisted of:

1. An authorized account-administration action occurred in Active Directory.
2. `DC01` recorded the action in the Windows Security log.
3. Windows logging and forwarding made the event available for collection.
4. The Splunk forwarder transmitted the event to Splunk Enterprise.
5. Splunk indexed the event as `XmlWinEventLog:Security`.
6. SPL detection logic filtered the relevant Event IDs.
7. The Splunk dashboard displayed the account-administration activity.
8. The event was reviewed and compared with Windows Event Viewer for validation.

## Security Use Cases

### 1. User-Account Creation Monitoring

Event ID `4720` identifies the creation of a user account.

Monitoring this event helps analysts determine:

* Which account was created
* When the account was created
* Which administrator performed the action
* Which domain or system recorded the event
* Whether the new identity was authorized
* Whether the account was created outside the normal provisioning process

Unexpected account creation can indicate unauthorized persistence, insider activity, compromised administrator credentials, or a failure in identity-governance procedures.

### 2. Account-Enablement Monitoring

Event ID `4722` identifies the enablement of a user account.

Monitoring this event helps identify:

* Reactivation of dormant accounts
* Re-enablement of previously disabled users
* Changes involving terminated or transferred employees
* Unexpected restoration of access
* Administrative activity requiring review

An enabled account should have an approved business purpose and an authorized administrator.

### 3. Password-Reset Monitoring

Event ID `4724` records an attempt to reset another account’s password.

Monitoring this event helps analysts review:

* Administrative password-reset activity
* Resets involving privileged accounts
* Unexpected help-desk or administrator actions
* Potential credential takeover
* Identity-recovery activity
* Password resets outside normal operating hours

A password reset may be legitimate, but it should be validated against an approved request or administrative workflow.

### 4. Account-Disablement Monitoring

Event ID `4725` identifies the disablement of a user account.

Monitoring this event supports:

* Employee offboarding
* Containment of suspected compromised accounts
* Access suspension
* Identity-lifecycle validation
* Review of unexpected administrative action

Unexpected disablement can interrupt business operations or indicate misuse of administrative privileges.

## Implementation

### 1. Account-Management Auditing

* Confirmed that Windows account-management auditing was enabled
* Verified that Active Directory administrative actions generated security events
* Reviewed Event IDs `4720`, `4722`, `4724`, and `4725`
* Confirmed that the events contained useful identity and administrative context

### 2. Windows Log Collection

* Collected Windows Security events from `DC01`
* Verified that the domain-controller logs were forwarded for centralized monitoring
* Confirmed that the data reached Splunk Enterprise
* Verified ingestion under `XmlWinEventLog:Security`
* Confirmed that the required account-administration Event IDs were searchable

### 3. SPL Detection Development

Developed and validated SPL logic to:

* Search the Windows Security event data
* Filter events to the relevant account-management Event IDs
* Identify the affected account
* Identify the administrator or initiating account when available
* Review the event timestamp and source host
* Categorize events by administrative action
* Count account-administration events
* Support dashboard visualization and investigation

### 4. Dashboard Development

Created and finalized a Splunk dashboard for Active Directory account administration.

The dashboard enabled centralized review of:

* User-account creation
* Account enablement
* Password-reset attempts
* Account disablement
* Activity over time
* Events by account
* Events by administrator
* Events by host
* Detailed records for investigation

### 5. Dashboard Validation

Validated the dashboard by:

* Confirming that the expected events existed in Windows Event Viewer
* Verifying ingestion into Splunk
* Running the underlying SPL searches
* Confirming that the four required Event IDs were represented
* Comparing dashboard values with the underlying search results
* Reviewing the applicable time range
* Confirming that dashboard panels displayed account-administration activity

## Relevant Event Fields

The following fields are useful during an investigation:

| Field            | Investigative Value                                         |
| ---------------- | ----------------------------------------------------------- |
| Event ID         | Identifies the administrative action                        |
| Target account   | Identifies the account affected by the action               |
| Subject account  | Identifies the user or process that initiated the action    |
| Domain name      | Identifies the associated Active Directory domain           |
| Computer name    | Identifies the system that recorded the event               |
| Timestamp        | Establishes when the action occurred                        |
| Subject logon ID | Helps correlate the action with the administrator’s session |
| Account status   | Provides context for enablement or disablement              |
| Host             | Identifies the Splunk event source                          |
| Sourcetype       | Identifies the Windows event-data format                    |

Field availability can differ by Event ID and Windows event format.

## Validation Activities

### Source-Event Validation

* Opened Windows Event Viewer
* Reviewed the Security log on the domain controller
* Located the applicable account-management events
* Confirmed the Event IDs and timestamps
* Reviewed the affected and initiating accounts
* Compared the original Windows records with Splunk

### Splunk Ingestion Validation

* Confirmed that `DC01` appeared as the event source
* Verified the `XmlWinEventLog:Security` sourcetype
* Confirmed that Event IDs `4720`, `4722`, `4724`, and `4725` were searchable
* Reviewed timestamps and available identity fields
* Verified that the events matched the original Windows records

### Dashboard Validation

* Confirmed that the dashboard loaded successfully
* Reviewed the selected time range
* Confirmed that the dashboard displayed the expected event categories
* Compared panel results with the underlying SPL searches
* Verified that the account-administration events were represented correctly
* Confirmed that detailed event records were available for investigation

### Detection-Quality Validation

* Confirmed that the searches were limited to the intended account-management events
* Verified that each Event ID was mapped to the correct administrative action
* Reviewed affected-account and administrator context
* Confirmed that the dashboard supported analyst interpretation

## Detection Logic

The detection follows this analytical pattern:

* **Data source:** Windows Security logs
* **Sourcetype:** `XmlWinEventLog:Security`
* **Source system:** `DC01`
* **Event filters:** `4720`, `4722`, `4724`, and `4725`
* **Analysis:** Categorize account-administration actions
* **Context:** Review affected account, administrator, host, and time
* **Output:** Dashboard visualizations and detailed investigation results

The exact SPL should be published only after it has been copied directly from the validated Splunk search and checked for accuracy.

## Investigation Workflow

When an account-administration event is detected, the analyst should:

1. Identify the Event ID and administrative action.
2. Record the timestamp and domain controller.
3. Identify the affected account.
4. Identify the administrator or initiating identity.
5. Determine whether the account is standard, privileged, or service-related.
6. Review related account-management events.
7. Check for an approved service request or change record.
8. Review authentication activity associated with the initiating identity.
9. Determine whether the action was authorized.
10. Escalate or contain suspicious activity.
11. Document the findings and response actions.

## Security Analysis

### Indicators That May Require Investigation

* Account creation outside the approved provisioning process
* Enablement of a dormant or terminated user account
* Password reset involving a privileged account
* Multiple administrative changes within a short period
* Activity performed outside normal business hours
* Actions initiated by an unexpected administrator
* Account changes followed by suspicious authentication
* Administrative activity with no corresponding approval record

### Potential Benign Causes

* Approved employee onboarding
* Account reactivation
* Help-desk password assistance
* Planned administrative maintenance
* Employee offboarding
* Security containment
* Authorized identity-lifecycle activity
* Controlled CyberLab validation

An account-management event is an investigative signal and does not, by itself, prove malicious activity.

## Analyst Response Guidance

Depending on the investigation findings, appropriate actions may include:

* Verify the action with the responsible administrator
* Review the associated service request
* Disable an unauthorized account
* Reset credentials
* Revoke active sessions
* Remove unnecessary privileges
* Review related authentication events
* Examine activity performed by the affected account
* Preserve the relevant Windows and Splunk evidence
* Escalate confirmed suspicious activity
* Document corrective actions and lessons learned

## MITRE ATT&CK Mapping

| Tactic               | Technique                                  | Relevance                                                                  |
| -------------------- | ------------------------------------------ | -------------------------------------------------------------------------- |
| Persistence          | T1136.002 — Create Account: Domain Account | Event ID `4720` may identify unauthorized domain-account creation          |
| Persistence          | T1098 — Account Manipulation               | Account enablement or modification may support persistent access           |
| Privilege Escalation | T1098 — Account Manipulation               | Identity changes may be used to maintain or increase access                |
| Defense Evasion      | T1078 — Valid Accounts                     | Modified or re-enabled accounts may support unauthorized valid-account use |

MITRE ATT&CK mappings provide investigative context. The Windows events alone do not prove that an ATT&CK technique occurred.

## Tools and Technologies Used

| Tool or Technology                   | Purpose                                                 |
| ------------------------------------ | ------------------------------------------------------- |
| Windows Server 2025                  | Hosted the Active Directory domain controller           |
| Active Directory Domain Services     | Provided centralized identity administration            |
| Active Directory Users and Computers | Supported user-account administration                   |
| Windows Security Log                 | Recorded account-management events                      |
| Windows Event Viewer                 | Validated the original Windows events                   |
| Windows Event Forwarding             | Supported centralized event collection                  |
| Splunk Forwarder                     | Sent Windows Security events to Splunk                  |
| Splunk Enterprise                    | Searched, analyzed, and visualized the events           |
| SPL                                  | Filtered, categorized, and summarized account activity  |
| Splunk Dashboards                    | Presented centralized account-administration visibility |
| VMware Workstation                   | Hosted the CyberLab virtual systems                     |
| Wazuh                                | Provided complementary endpoint-monitoring visibility   |
| GitHub                               | Published sanitized documentation and evidence          |

## Security Skills Demonstrated

* Active Directory security monitoring
* Identity and access management monitoring
* Windows account-management auditing
* Splunk Enterprise administration
* Windows log ingestion
* SPL detection development
* Dashboard development
* Detection validation
* User-account lifecycle monitoring
* Privileged-activity investigation
* Windows Event ID analysis
* SIEM investigation
* MITRE ATT&CK mapping
* False-positive analysis
* Incident-triage planning
* Evidence sanitization
* Technical security documentation

## Project Results

The project successfully demonstrated:

* Windows account-management auditing
* Centralized ingestion of Active Directory events into Splunk
* Monitoring of Event ID `4720` for user creation
* Monitoring of Event ID `4722` for account enablement
* Monitoring of Event ID `4724` for password-reset attempts
* Monitoring of Event ID `4725` for account disablement
* A completed and validated Splunk dashboard
* Analyst visibility into affected accounts and administrative actions
* A repeatable workflow for investigating identity changes
* A foundation for expanded Active Directory monitoring

## Security Value

This monitoring capability supports:

* Detection of unauthorized account creation
* Review of dormant-account reactivation
* Investigation of privileged password resets
* Employee onboarding and offboarding validation
* Identity-governance oversight
* Insider-threat monitoring
* Privileged-account monitoring
* Incident investigation and response
* Compliance and audit readiness

## Evidence

The following sanitized evidence should support the completed project:

### Windows Event Evidence

* Event ID `4720` showing user-account creation
* Event ID `4722` showing account enablement
* Event ID `4724` showing a password-reset attempt
* Event ID `4725` showing account disablement
* Relevant timestamps and sanitized identity information

### Splunk Ingestion Evidence

* `XmlWinEventLog:Security` data from `DC01`
* Relevant account-management Event IDs
* Extracted target and subject account information
* Event timestamps and source-host details

### SPL Search Evidence

* Search results for the four account-administration Event IDs
* Categorized administrative actions
* Activity summarized by account, administrator, host, or time
* Detailed records supporting investigation

### Dashboard Evidence

* Completed Active Directory account-administration dashboard
* Panels displaying account creation
* Panels displaying account enablement
* Panels displaying password-reset attempts
* Panels displaying account disablement
* Dashboard time range and validated results

> **Evidence notice:** Passwords, IP addresses, personal information, account identifiers, security identifiers, logon IDs, internal addresses, and unnecessary infrastructure details must be removed or obscured before screenshots are published.

## Challenges and Resolutions

### Events Not Appearing in the Dashboard

**Challenge:** Expected account-management events may not appear when the wrong time range, host, sourcetype, or Event ID is selected.

**Resolution:** Confirmed the original events in Windows Event Viewer, reviewed the Splunk time range, and validated the underlying searches before refreshing the dashboard.

### Identifying the Initiating Administrator

**Challenge:** The affected account and initiating account can be confused during event analysis.

**Resolution:** Reviewed the subject and target sections of the Windows event separately to distinguish the administrator from the affected user.

### Event Meaning and Context

**Challenge:** An account-management event can represent either authorized administration or suspicious activity.

**Resolution:** Evaluated the administrator, affected account, timestamp, business justification, and surrounding authentication activity before assigning security significance.

### Dashboard Accuracy

**Challenge:** A dashboard visualization can be misleading if its underlying search is incomplete.

**Resolution:** Validated each underlying search and compared dashboard results with the original Windows events.

### Sensitive Information in Evidence

**Challenge:** Account-management screenshots can expose usernames, domain information, security identifiers, and internal infrastructure details.

**Resolution:** Sanitized the evidence while preserving the technical information required to demonstrate the detection.

## Lessons Learned

* Active Directory account-management events provide important identity-security visibility.
* Event IDs must be interpreted together with subject and target account information.
* Account creation and enablement should be validated against approved identity-lifecycle processes.
* Privileged-account password resets require additional scrutiny.
* Windows Event Viewer is essential for validating the original source event.
* Splunk dashboards improve visibility, but the underlying SPL searches must be validated.
* Time-range selection strongly affects detection and dashboard results.
* Administrative activity is not automatically malicious and must be evaluated in context.
* Controlled testing helps confirm that the monitoring workflow operates correctly.
* Sanitized evidence strengthens the credibility of a public cybersecurity portfolio.

## Current Scope and Future Extension

The completed project monitors:

* Event ID `4720`
* Event ID `4722`
* Event ID `4724`
* Event ID `4725`

The following group-membership events are planned as a future extension and are not represented as completed in this project:

* Member added to a security group
* Member removed from a security group
* Changes involving privileged Active Directory groups
* Correlation of group-membership changes with administrator authentication

## Security and Privacy Statement

* All activity was performed in an isolated and authorized CyberLab.
* No production systems or third-party accounts were accessed.
* Test identities and controlled administrative actions were used for validation.
* Sensitive information is removed or obscured before evidence is published.

## Related CyberLab Projects

* Active Directory Security and Domain Controller Administration
* Windows Security Logging and Event Forwarding
* Splunk SIEM Deployment and Detection Engineering
* Wazuh SIEM and Endpoint Monitoring
* Failed Logon Detection
* Active Directory Account Lockout Detection
* Password Spray Detection
* Privileged Account Monitoring
