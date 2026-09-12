# Splunk SIEM Deployment & Detection Engineering

## Project Overview

This project demonstrates the deployment and configuration of Splunk Enterprise as a Security Information and Event Management platform in a Windows Active Directory CyberLab.

Windows security events were ingested into Splunk through forwarders and analyzed using Search Processing Language (SPL), dashboards, reports, and alerts. The project established centralized visibility into authentication activity, account lockouts, Active Directory account administration, and other security-relevant Windows events.

## Project Status

✅ Completed

## Project Objectives

* Deploy Splunk Enterprise in the CyberLab
* Configure Splunk forwarders for Windows systems
* Ingest Windows security-event data
* Verify host, source, sourcetype, and event metadata
* Develop SPL searches for security investigations
* Monitor successful and failed authentication
* Detect account-lockout activity
* Monitor Active Directory account-administration events
* Create and validate security dashboards
* Configure alerts for security-relevant activity
* Correlate related Windows events
* Document the implementation with sanitized evidence

## Lab Environment

| Component                                | Purpose                                                         |
| ---------------------------------------- | --------------------------------------------------------------- |
| VMware Workstation                       | Hosted the virtual CyberLab systems                             |
| Windows Server 2025 — `DC01`             | Provided Active Directory and Windows security events           |
| Windows 11 Enterprise — `WIN11-CLIENT01` | Generated endpoint and authentication events                    |
| Active Directory — `cyberlab.local`      | Provided centralized identity and authentication                |
| Splunk Enterprise                        | Centralized event collection, searching, dashboards, and alerts |
| Splunk Forwarders                        | Sent Windows event data to Splunk Enterprise                    |
| Windows Event Logs                       | Provided authentication and account-management telemetry        |
| SPL                                      | Supported searching, filtering, correlation, and visualization  |
| Wazuh                                    | Provided complementary endpoint-security visibility             |

## Architecture and Data Flow

The completed monitoring workflow consisted of:

1. Windows systems generated authentication, account-management, and security events.
2. Splunk forwarders collected the configured Windows event logs.
3. Events were transmitted to Splunk Enterprise.
4. Splunk parsed and indexed the incoming events.
5. SPL searches filtered and analyzed security-relevant activity.
6. Dashboards displayed authentication and identity trends.
7. Alerts supported investigation of suspicious or policy-relevant events.
8. Correlation searches connected related events into security use cases.

## Implementation

### 1. Splunk Enterprise Deployment

* Installed Splunk Enterprise in the CyberLab
* Started and verified the Splunk services
* Accessed the Splunk web interface
* Confirmed that the platform was available for data ingestion and analysis
* Reviewed Splunk search, dashboard, alert, and data-management capabilities

### 2. Forwarder Configuration

* Installed and configured Splunk forwarders on the applicable Windows systems
* Connected the forwarders to Splunk Enterprise
* Configured collection of relevant Windows event channels
* Verified communication between the Windows systems and Splunk
* Confirmed that expected hosts appeared in the Splunk data

### 3. Windows Event-Log Ingestion

Configured Splunk to ingest security-relevant Windows event data, including:

* Authentication events
* Account-lockout events
* Account-management events
* Privileged-logon events
* PowerShell events
* Other Windows security events required for monitoring and investigation

Ingested events were reviewed to verify important metadata such as:

* Event ID
* Host
* Source
* Sourcetype
* Timestamp
* Account name
* Computer name
* Logon type
* Source workstation or address, when available

### 4. SPL Search Development

Developed and validated SPL searches to:

* Locate Windows security events
* Filter activity by Event ID
* Review events by host and account
* Count security events over time
* Identify repeated failed-logon attempts
* Investigate locked accounts
* Monitor Active Directory account changes
* Compare activity across systems
* Extract useful fields for dashboards
* Support event correlation and investigation

### 5. Failed-Logon Detection

Created and validated detection logic for Windows Event ID `4625`.

Event ID `4625` records failed account-logon activity and can help identify:

* Incorrect password attempts
* Authentication failures
* Repeated failed logons
* Possible brute-force activity
* Possible password-spray activity
* Misconfigured services or scheduled tasks
* Attempts involving disabled or restricted accounts

The detection workflow included:

* Generating controlled failed-logon events
* Confirming that the events appeared in Windows Event Viewer
* Verifying ingestion into Splunk
* Filtering the events by Event ID
* Reviewing the affected account, host, time, and available source information
* Visualizing failed-logon activity
* Preserving relevant evidence for portfolio documentation

### 6. Account-Lockout Detection and Correlation

Created and validated an Active Directory account-lockout use case using:

| Event ID | Security Significance              |
| -------: | ---------------------------------- |
|     4771 | Kerberos pre-authentication failed |
|     4740 | A user account was locked out      |

The investigation connected authentication failures with the resulting account lockout. This demonstrated how related events can be correlated to reconstruct an identity-security incident.

The completed workflow included:

* Generating controlled authentication failures
* Triggering an account lockout
* Identifying the affected user account
* Reviewing the event sequence
* Correlating Event IDs `4771` and `4740`
* Validating the activity in Splunk
* Documenting the investigation as a GitHub case study

### 7. Active Directory Account-Administration Monitoring

Created dashboard monitoring for important Active Directory account-administration events:

| Event ID | Description                          |
| -------: | ------------------------------------ |
|     4720 | User account created                 |
|     4722 | User account enabled                 |
|     4724 | Attempt to reset an account password |
|     4725 | User account disabled                |

Monitoring these events improves visibility into the identity lifecycle and helps identify unexpected or unauthorized administrative changes.

### 8. Dashboard Development

Created and validated Splunk dashboards to provide centralized security visibility.

Dashboard content included security-relevant views such as:

* Windows security-event activity
* Failed-logon activity
* Authentication trends
* Account-lockout events
* Active Directory account-administration events
* Event counts over time
* Activity by user or host
* Data-ingestion and source validation

The dashboards converted raw Windows events into visual information that could be reviewed quickly during monitoring and investigation.

### 9. Alert Configuration

Configured Splunk alerts for selected security-relevant searches.

The alerting workflow included:

* Defining the triggering search
* Selecting the appropriate time range
* Establishing the alert condition
* Reviewing the result fields
* Validating the alert with controlled lab activity
* Confirming that the alert supported the related investigation workflow

### 10. Detection Validation

Each detection was validated through controlled CyberLab activity.

The general validation process was:

1. Generate the expected activity on a Windows system.
2. Confirm the event in Windows Event Viewer.
3. Verify that the event was ingested into Splunk.
4. Run the applicable SPL search.
5. Confirm that the expected fields were present.
6. Review the related dashboard panel or alert.
7. Compare the results with the original Windows event.
8. Capture sanitized evidence.

## Completed Detection Use Cases

| Detection Use Case                         | Relevant Event IDs | Status      |
| ------------------------------------------ | ------------------ | ----------- |
| Successful logon monitoring                | 4624               | ✅ Validated |
| Failed-logon detection                     | 4625               | ✅ Validated |
| Kerberos authentication-failure analysis   | 4771               | ✅ Validated |
| Active Directory account-lockout detection | 4740               | ✅ Validated |
| Account creation monitoring                | 4720               | ✅ Validated |
| Account enablement monitoring              | 4722               | ✅ Validated |
| Password-reset monitoring                  | 4724               | ✅ Validated |
| Account-disablement monitoring             | 4725               | ✅ Validated |

## Validation Activities

### Splunk Service Validation

* Confirmed that Splunk Enterprise was running
* Verified access to the Splunk web interface
* Confirmed that search and dashboard functions were available

### Forwarder Validation

* Verified communication between the Windows systems and Splunk
* Confirmed that expected hosts appeared in search results
* Verified continued Windows event ingestion

### Data-Ingestion Validation

* Reviewed recently indexed Windows events
* Confirmed timestamps and host information
* Verified that security Event IDs were searchable
* Confirmed that expected Windows event fields were available
* Compared selected Splunk events with Windows Event Viewer

### SPL Validation

* Executed security-focused SPL searches
* Confirmed that filters returned the intended Event IDs
* Reviewed results by user, host, and time
* Verified that searches supported investigation and visualization

### Dashboard Validation

* Confirmed that dashboard panels loaded successfully
* Verified that dashboard results reflected the ingested events
* Tested the dashboards using controlled security activity
* Reviewed time ranges and event counts
* Confirmed that dashboard data matched related search results

### Detection Validation

* Generated failed-logon activity
* Verified Event ID `4625` in Splunk
* Generated and investigated account-lockout activity
* Correlated Event IDs `4771` and `4740`
* Reviewed account-administration events
* Confirmed monitoring of Event IDs `4720`, `4722`, `4724`, and `4725`

## Tools and Technologies Used

| Tool or Technology               | Purpose                                                     |
| -------------------------------- | ----------------------------------------------------------- |
| Splunk Enterprise                | Centralized event ingestion, search, dashboards, and alerts |
| Splunk Forwarders                | Collected and transmitted Windows event data                |
| Search Processing Language       | Filtered, analyzed, correlated, and visualized events       |
| Windows Event Viewer             | Validated the original Windows events                       |
| Windows Server 2025              | Generated Active Directory and security events              |
| Windows 11 Enterprise            | Generated endpoint and authentication activity              |
| Active Directory Domain Services | Provided identity and authentication services               |
| Group Policy                     | Supported centralized Windows audit configuration           |
| PowerShell                       | Supported event generation, administration, and validation  |
| VMware Workstation               | Hosted the CyberLab systems                                 |
| Wazuh                            | Provided complementary endpoint-monitoring visibility       |
| GitHub                           | Published sanitized project documentation and evidence      |

## Security Skills Demonstrated

* Splunk Enterprise deployment and administration
* SIEM data onboarding
* Windows event-log ingestion
* Splunk forwarder configuration
* SPL search development
* Detection engineering
* Windows authentication monitoring
* Active Directory security monitoring
* Failed-logon detection
* Account-lockout investigation
* Event correlation
* Identity-event monitoring
* Dashboard design and validation
* Security-alert configuration
* Event-field analysis
* Detection testing
* Security investigation
* Evidence collection and sanitization
* Technical documentation

## Project Results

The project established a functional Splunk-based security-monitoring capability within the CyberLab.

Completed outcomes included:

* Splunk Enterprise deployment
* Splunk forwarder configuration
* Windows security-log ingestion
* Searchable authentication and account-management events
* Security-focused SPL searches
* Validated dashboard panels
* Alert configuration
* Failed-logon detection using Event ID `4625`
* Account-lockout investigation using Event IDs `4771` and `4740`
* Active Directory account-administration monitoring using Event IDs `4720`, `4722`, `4724`, and `4725`
* A documented GitHub account-lockout case study
* A reusable foundation for additional detection-engineering and incident-response exercises

## Evidence

The project evidence should include sanitized screenshots of the following:

### Splunk Deployment

* Splunk Enterprise web interface
* Splunk service availability
* Connected or reporting Windows hosts

### Windows Data Ingestion

* Windows security events displayed in Splunk
* Event metadata such as Event ID, host, source, sourcetype, and timestamp
* Comparison between a Windows event and its corresponding Splunk record

### SPL Searches

* Failed-logon search results
* Account-lockout search results
* Authentication activity grouped by account or host
* Active Directory account-administration search results

### Dashboards

* Completed Splunk security dashboard
* Failed-logon dashboard panel
* Account-lockout activity
* Active Directory account-administration monitoring
* Event trends and counts

### Detection Validation

* Event ID `4625` displayed in Splunk
* Event IDs `4771` and `4740` displayed in the account-lockout investigation
* Event IDs `4720`, `4722`, `4724`, and `4725` displayed in account-administration monitoring
* Controlled test activity matching the detection results

### Alerts

* Configured Splunk alert
* Alert trigger or corresponding search results
* Validated event details supporting the alert

> **Evidence notice:** All screenshots must be sanitized before publication. Passwords, IP addresses, personal information, account identifiers, session identifiers, and unnecessary system or resource identifiers must be removed or obscured.

## Challenges and Resolutions

### Windows Events Not Appearing in Splunk

**Challenge:** Expected Windows events were not immediately visible in the search results.

**Resolution:** Verified that the original event existed in Windows Event Viewer, checked forwarder communication, reviewed the selected time range, and confirmed that the correct Windows event channel was being collected.

### Search Results Did Not Match the Expected Activity

**Challenge:** Broad searches returned unrelated events or failed to isolate the intended activity.

**Resolution:** Refined the search using the relevant Event ID, host, account, and time range, then compared the results with the original Windows event.

### Dashboard Evidence Did Not Appear

**Challenge:** A dashboard panel did not initially display the expected evidence.

**Resolution:** Validated the underlying SPL search, reviewed the time picker, confirmed data availability, and refreshed the dashboard after generating controlled activity.

### Account-Lockout Correlation

**Challenge:** A single event did not provide the complete sequence leading to an account lockout.

**Resolution:** Correlated Kerberos authentication-failure Event ID `4771` with account-lockout Event ID `4740` to reconstruct the event sequence.

### Sensitive Information in Screenshots

**Challenge:** Splunk events and dashboards could expose usernames, addresses, identifiers, and infrastructure details.

**Resolution:** Sanitized screenshots before publication while preserving the fields necessary to demonstrate the detection and investigation.

## Lessons Learned

* Effective SIEM monitoring begins with reliable data ingestion.
* Windows Event Viewer is essential for validating the source event before troubleshooting Splunk.
* Time-range selection can determine whether relevant events appear in a search or dashboard.
* Event IDs provide useful starting points, but context from user, host, timestamp, and related events is necessary for investigation.
* SPL searches should be validated before they are converted into dashboard panels or alerts.
* Controlled testing is necessary to confirm that detections work as intended.
* Dashboards support situational awareness, while detailed searches support investigation.
* Correlating multiple events provides better context than reviewing isolated events.
* Failed authentication does not always represent malicious activity and must be investigated in context.
* Identity lifecycle events are important for detecting unauthorized administrative changes.
* Clear documentation and sanitized evidence make technical work easier for recruiters and hiring managers to evaluate.

## Security and Privacy Statement

* All activity was performed in an isolated and authorized CyberLab.
* No production systems or third-party accounts were accessed.
* Test accounts and controlled activity were used for validation.
* Sensitive data is removed or obscured before evidence is published.

## Related CyberLab Projects

* Active Directory Security and Domain Controller Administration
* Windows Security Logging and Event Forwarding
* Wazuh SIEM and Endpoint Monitoring
* Failed Logon Detection
* Active Directory Account Lockout Detection
* Password Spray Detection
* Brute-Force Authentication Detection
* Privileged Account Monitoring
