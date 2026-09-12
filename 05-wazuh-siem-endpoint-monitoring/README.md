# Wazuh SIEM & Endpoint Monitoring

## Project Overview

This project demonstrates the deployment and validation of Wazuh for centralized security monitoring in a Windows Active Directory CyberLab.

The Wazuh manager and indexer were deployed, and a Wazuh agent was installed and enrolled on the Windows Server 2025 domain controller named `DC01`. Endpoint events from the domain controller were successfully collected and made visible in Wazuh for centralized analysis.

## Project Status

✅ Completed

## Project Objectives

* Deploy the Wazuh security-monitoring platform
* Configure the Wazuh manager and indexer
* Install the Wazuh agent on `DC01`
* Enroll and connect the endpoint agent to the Wazuh manager
* Collect endpoint and Windows security telemetry
* Verify agent health and connectivity
* Confirm that events from `DC01` were visible in Wazuh
* Establish centralized endpoint-security visibility
* Prepare the environment for additional detection and investigation use cases
* Document the project with sanitized technical evidence

## Lab Environment

| Component                | Configuration                      |
| ------------------------ | ---------------------------------- |
| Hypervisor               | VMware Workstation                 |
| Active Directory Domain  | `cyberlab.local`                   |
| Monitored Endpoint       | Windows Server 2025 — `DC01`       |
| Endpoint Role            | Active Directory domain controller |
| Endpoint Sensor          | Wazuh agent                        |
| Central Management       | Wazuh manager                      |
| Event Storage and Search | Wazuh indexer                      |
| Local Event Validation   | Windows Event Viewer               |
| Complementary SIEM       | Splunk Enterprise                  |

## Monitoring Architecture

The completed monitoring workflow consisted of:

1. `DC01` generated Windows and endpoint-security events.
2. The Wazuh agent collected configured endpoint telemetry.
3. The agent transmitted the data to the Wazuh manager.
4. The Wazuh manager received and processed the endpoint data.
5. The Wazuh indexer stored the processed security events.
6. Wazuh provided centralized visibility into events originating from `DC01`.
7. Selected events could be compared with Windows Event Viewer and Splunk for validation.

## Implementation

### 1. Wazuh Platform Deployment

* Deployed the Wazuh manager
* Deployed the Wazuh indexer
* Verified that the required Wazuh services were available
* Confirmed that the central Wazuh components could process endpoint data
* Accessed the Wazuh monitoring interface

### 2. Domain Controller Preparation

* Identified Windows Server 2025 `DC01` as the monitored endpoint
* Confirmed that the domain controller had network connectivity to the Wazuh platform
* Verified that Windows security events were available locally
* Prepared the system for Wazuh agent installation

### 3. Wazuh Agent Installation

* Installed the Wazuh agent on `DC01`
* Configured the agent to communicate with the Wazuh manager
* Registered the domain controller as a monitored endpoint
* Started the Wazuh agent service
* Confirmed that the agent remained operational

### 4. Agent Enrollment and Connectivity

* Enrolled the `DC01` agent with the Wazuh manager
* Verified that the endpoint appeared in the Wazuh agent inventory
* Confirmed that the agent reported as connected
* Validated communication between the agent and the manager
* Confirmed that endpoint data reached the Wazuh platform

### 5. Endpoint-Event Collection

Configured and validated the collection of security-relevant endpoint telemetry from `DC01`.

The available telemetry supported visibility into areas such as:

* Windows security activity
* Authentication activity
* Account-management activity
* Administrative operations
* System activity
* Endpoint status
* Security-relevant configuration and log data

### 6. Centralized Event Visibility

* Reviewed endpoint events received from `DC01`
* Confirmed that the monitored agent was identified as the event source
* Reviewed event timestamps and available security context
* Verified that endpoint activity was searchable and available for analysis
* Compared selected activity with the original Windows event source when necessary

### 7. Integration with the Wider CyberLab

The Wazuh implementation complemented the existing CyberLab monitoring architecture by providing endpoint-focused visibility alongside:

* Windows Event Viewer
* Windows Event Forwarding
* Splunk Enterprise
* Active Directory security monitoring
* Authentication-event analysis
* Account-lockout investigation

## Validation Activities

### Wazuh Service Validation

* Confirmed that the Wazuh manager was available
* Confirmed that the Wazuh indexer was available
* Verified access to the Wazuh monitoring interface
* Confirmed that the platform could receive and display endpoint data

### Agent Validation

* Verified that the Wazuh agent service was running on `DC01`
* Confirmed that `DC01` appeared in the Wazuh agent inventory
* Verified that the agent reported a connected or active status
* Confirmed communication between the agent and Wazuh manager

### Event-Collection Validation

* Generated or reviewed security-relevant activity on `DC01`
* Confirmed that the corresponding events were available locally
* Verified that endpoint events appeared in Wazuh
* Reviewed the event source, endpoint name, timestamp, and available security details
* Confirmed that the displayed events originated from the expected endpoint

### Cross-Platform Validation

Where applicable, selected endpoint events were compared across:

* Windows Event Viewer
* Wazuh
* Splunk Enterprise

This comparison helped confirm that endpoint activity was being collected and represented consistently across the CyberLab monitoring platforms.

## Tools and Technologies Used

| Tool or Technology               | Purpose                                                    |
| -------------------------------- | ---------------------------------------------------------- |
| Wazuh Manager                    | Received, processed, and managed endpoint-security data    |
| Wazuh Indexer                    | Stored and supported searches of processed security events |
| Wazuh Agent                      | Collected telemetry from `DC01`                            |
| Windows Server 2025              | Hosted the monitored Active Directory domain controller    |
| Active Directory Domain Services | Provided identity and authentication activity              |
| Windows Event Viewer             | Supported local event validation                           |
| VMware Workstation               | Hosted the CyberLab virtual systems                        |
| Splunk Enterprise                | Provided complementary SIEM visibility and event analysis  |

## Security Skills Demonstrated

* Wazuh deployment and administration
* Endpoint-agent installation
* Agent enrollment and lifecycle management
* SIEM and endpoint-monitoring architecture
* Centralized security-event collection
* Windows Server monitoring
* Active Directory security visibility
* Endpoint telemetry analysis
* Agent-health validation
* Event-source validation
* Security monitoring and investigation
* Cross-platform event comparison
* Troubleshooting endpoint connectivity
* Evidence collection and sanitization
* Technical security documentation

## Project Results

The project established a functioning Wazuh endpoint-monitoring capability within the CyberLab.

Completed outcomes included:

* Wazuh manager deployment
* Wazuh indexer deployment
* Wazuh agent installation on `DC01`
* Successful enrollment of the domain controller
* Confirmed agent connectivity
* Centralized collection of endpoint events
* Security-event visibility in Wazuh
* A foundation for additional endpoint-detection and investigation use cases
* Complementary monitoring alongside Splunk Enterprise and Windows Event Forwarding

## Security Value

The project demonstrates how centralized endpoint monitoring can improve security operations by:

* Providing visibility into monitored systems
* Centralizing endpoint-security telemetry
* Supporting authentication and identity investigations
* Helping analysts review activity without accessing each endpoint individually
* Supporting comparisons between local and centralized event records
* Establishing the telemetry foundation required for detection engineering
* Improving readiness for incident investigation and response

## Evidence

The following sanitized evidence should support the project:

### Wazuh Platform

* Wazuh monitoring interface
* Wazuh manager availability
* Wazuh indexer availability

### Agent Installation and Enrollment

* Wazuh agent installed on `DC01`
* Wazuh agent service running
* `DC01` displayed in the Wazuh agent inventory
* Agent status displayed as connected or active

### Endpoint-Event Visibility

* Security events originating from `DC01`
* Event details showing the monitored endpoint
* Event timestamps and relevant security context
* Search or filtered view of endpoint activity

### Cross-Platform Validation

* Original event displayed in Windows Event Viewer
* Corresponding endpoint activity displayed in Wazuh
* Related Splunk event, when available

> **Evidence notice:** All screenshots must be sanitized before publication. Passwords, IP addresses, personal information, account identifiers, agent identifiers, and unnecessary infrastructure details must be removed or obscured.

## Challenges and Resolutions

### Agent Connectivity

**Challenge:** Endpoint monitoring depended on reliable communication between the `DC01` agent and the Wazuh manager.

**Resolution:** Verified network connectivity, reviewed the agent configuration, confirmed that the Wazuh agent service was running, and checked the agent status in the Wazuh platform.

### Endpoint Events Not Immediately Visible

**Challenge:** Newly generated or collected endpoint events were not always immediately visible.

**Resolution:** Confirmed the event locally, verified the agent’s connected status, reviewed the applicable time range, and refreshed the event view before continuing the investigation.

### Event-Source Identification

**Challenge:** Centralized monitoring can contain events from multiple sources, making it necessary to confirm the affected endpoint.

**Resolution:** Reviewed the endpoint name, agent information, timestamp, and available event metadata to confirm that the activity originated from `DC01`.

### Cross-Platform Event Differences

**Challenge:** The same activity could appear differently in Windows Event Viewer, Wazuh, and Splunk because each platform processes and presents event data differently.

**Resolution:** Compared the timestamp, endpoint, event information, and security context rather than relying only on the display format.

### Sensitive Information in Evidence

**Challenge:** Wazuh screenshots could expose account, agent, address, and infrastructure information.

**Resolution:** Sanitized screenshots before publication while retaining the technical information required to demonstrate successful monitoring.

## Lessons Learned

* Endpoint monitoring depends on reliable agent-to-manager communication.
* Agent status should be verified before troubleshooting missing events.
* Local Windows logs provide an important reference for validating centralized telemetry.
* Endpoint name, timestamp, and event context help confirm the origin of activity.
* Time-range selection affects whether events appear during an investigation.
* Wazuh and Splunk provide complementary views of security activity.
* Centralized endpoint telemetry creates a foundation for detection engineering and incident response.
* Monitoring tools must be tested with controlled activity to confirm that data is being collected.
* Security screenshots must be sanitized before publication.
* Clear project documentation helps recruiters connect hands-on work to operational security skills.

## Security and Privacy Statement

* All activity was performed in an isolated and authorized CyberLab.
* No production systems or third-party accounts were accessed.
* Test systems and controlled activity were used for validation.
* Sensitive information is removed or obscured before evidence is published.

## Related CyberLab Projects

* Active Directory Security and Domain Controller Administration
* Windows Security Logging and Event Forwarding
* Splunk SIEM Deployment and Detection Engineering
* Failed Logon Detection
* Active Directory Account Lockout Detection
* Password Spray Detection
* Privileged Account Monitoring
