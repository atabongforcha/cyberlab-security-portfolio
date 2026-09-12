# Active Directory Security & Domain Controller Administration

## Project Overview

This project demonstrates the deployment, administration, validation, and security hardening of a Windows Server 2025 Active Directory environment.

A domain controller named `DC01` was deployed in VMware Workstation and configured to provide centralized identity management, authentication, authorization, DNS, Group Policy, and security auditing for the `cyberlabrekt.local` domain. A Windows  chips is 11 Enterprise workstation named `WIN11-CLIENT:\/\/` was joined to the domain to validate domain authentication, DNS communication, and security-policy enforcement.

## Project Status

✅ Completed

## Project Objectives

* Deploy Windows Server 2025 as a domain controller
* Install Active Directory Domain Services (AD DS)
* Create the `cyberlab.local` forest and domain
* Configure Active Directory-integrated DNS
* Create a structured Organizational Unit hierarchy
* Create and manage users, groups, computers, service accounts, and administrative accounts
* Separate standard user accounts from privileged accounts
* Join a Windows 11 Enterprise workstation to the domain
* Configure security controls through Group Policy
* Enable authentication and PowerShell auditing
* Validate Active Directory, DNS, domain authentication, and Group Policy
* Prepare Windows security events for Splunk and Wazuh monitoring

## Lab Environment

| Component               | Configuration                            |
| ----------------------- | ---------------------------------------- |
| Hypervisor              | VMware Workstation                       |
| Domain Controller       | Windows Server 2025 — `DC01`             |
| Active Directory Domain | `cyberlab.local`                         |
| Client Workstation      | Windows 11 Enterprise — `WIN11-CLIENT01` |
| Directory Service       | Active Directory Domain Services         |
| Name Resolution         | Active Directory-integrated DNS          |
| Policy Management       | Group Policy                             |
| Event Validation        | Windows Event Viewer and PowerShell      |
| Centralized Monitoring  | Splunk Enterprise and Wazuh              |

## Environment Architecture

`DC01` provides the following core services:

* Active Directory Domain Services
* Active Directory-integrated DNS
* Centralized authentication
* Centralized authorization
* Group Policy management
* Windows security auditing

`WIN11-CLIENT01` serves as the domain-joined endpoint used to validate user authentication, DNS connectivity, Group Policy application, and Windows security-event generation.

## Implementation

### 1. Windows Server Deployment

* Created a Windows Server 2025 virtual machine in VMware Workstation
* Installed and updated the operating system
* Renamed the server `DC01`
* Assigned the server a static IP address
* Configured the appropriate DNS settings
* Verified network connectivity

### 2. Active Directory Domain Services Deployment

* Installed the Active Directory Domain Services server role
* Promoted `DC01` to a domain controller
* Created the `cyberlab.local` forest and domain
* Restarted the server after domain-controller promotion
* Verified that Active Directory services started successfully
* Confirmed that `DC01` operated as the domain controller

### 3. DNS Configuration

* Installed and configured DNS during the domain-controller deployment
* Verified the `cyberlab.local` DNS zone
* Configured the client workstation to use the domain controller for DNS
* Confirmed that domain systems could resolve `DC01`
* Validated name resolution between the domain controller and client workstation

### 4. Organizational Unit Design

Created a structured Organizational Unit hierarchy for:

* Users
* Groups
* Computers
* Servers
* Administrative accounts
* Service accounts
* Business departments

The OU structure supports Group Policy targeting, delegated administration, identity organization, access control, and separation of privileged accounts.

### 5. Identity and Access Administration

* Created domain user accounts
* Created global security groups, including groups such as `GG_IT_Admins`
* Assigned users to groups according to their responsibilities
* Organized users and groups within the appropriate OUs
* Separated standard user accounts from privileged administrative accounts
* Created dedicated locations for service accounts
* Applied least-privilege principles when assigning access

### 6. Computer Administration

* Created and organized computer objects
* Placed client and server systems in the appropriate OUs
* Used the OU structure to support targeted Group Policy application
* Verified that domain-joined systems appeared correctly in Active Directory

### 7. Windows 11 Domain Integration

* Deployed Windows 11 Enterprise as `WIN11-CLIENT01`
* Configured the workstation to use the domain DNS service
* Joined `WIN11-CLIENT01` to `cyberlab.local`
* Restarted the workstation after the domain join
* Signed in using a domain account
* Verified the authenticated identity using `whoami`
* Confirmed communication with `DC01`
* Verified that domain Group Policies were applied

### 8. Group Policy and Domain Hardening

Configured Group Policy controls addressing:

* Password protections
* Account-lockout protections
* Advanced security auditing
* Microsoft Defender Antivirus
* Windows Defender Firewall
* PowerShell logging
* Authentication monitoring
* Domain and endpoint security-policy enforcement

### 9. Security Auditing

Configured Windows auditing to support the monitoring and investigation of:

* Successful authentication
* Failed authentication
* Account-lockout activity
* Account-management changes
* Privileged activity
* PowerShell activity
* Domain security events

### 10. PowerShell Logging

Enabled PowerShell auditing to improve visibility into administrative and potentially suspicious activity.

| Event ID | Description                     |
| -------: | ------------------------------- |
|     4103 | PowerShell module logging       |
|     4104 | PowerShell script-block logging |
|      400 | PowerShell engine started       |
|      403 | PowerShell engine stopped       |
|      600 | PowerShell provider activity    |

### 11. Centralized Monitoring Preparation

Prepared the Active Directory environment for centralized security monitoring through:

* Windows Event Viewer
* Windows Event Forwarding
* Splunk Enterprise
* Wazuh endpoint monitoring
* Authentication-event analysis
* PowerShell activity monitoring
* Account-lockout investigation

## Validation Activities

### Active Directory Validation

* Opened Active Directory Users and Computers
* Verified the `cyberlab.local` domain
* Confirmed that the required OUs were present
* Verified user, group, computer, administrative, and service-account objects
* Confirmed that the objects were placed in their appropriate OUs

### Domain Controller Validation

* Verified that `DC01` was operating as the domain controller
* Confirmed that Active Directory Domain Services was available
* Verified access to the Active Directory administrative tools
* Confirmed that domain services remained operational following restart

### DNS Validation

* Verified the `cyberlab.local` DNS zone
* Confirmed that the Windows 11 client used the domain controller for DNS
* Tested name resolution between domain systems
* Verified that DNS supported domain joining and authentication

### Domain Membership Validation

* Confirmed that `WIN11-CLIENT01` joined `cyberlab.local`
* Verified that its computer account appeared in Active Directory
* Successfully authenticated using a domain account
* Used `whoami` to confirm the authenticated domain identity

### Group Policy Validation

The following commands were used to refresh and validate Group Policy:

* `gpupdate /force` — Forced an immediate Group Policy refresh
* `gpresult /r` — Displayed the policies applied to the user and computer
* `gpresult /h C:\Temp\gpresult.html` — Generated a detailed HTML Group Policy report

The results confirmed that the expected domain policies were applied to the workstation.

### Security-Event Validation

* Reviewed authentication events in Windows Event Viewer
* Confirmed the generation of failed-logon events
* Verified account-lockout activity
* Reviewed PowerShell operational events
* Confirmed that relevant Windows events were available for centralized monitoring

## Tools and Technologies Used

| Tool or Technology                   | Purpose                                                            |
| ------------------------------------ | ------------------------------------------------------------------ |
| VMware Workstation                   | Hosted the Windows Server and Windows 11 virtual machines          |
| Windows Server 2025                  | Hosted the Active Directory domain controller                      |
| Windows 11 Enterprise                | Served as the domain-joined client workstation                     |
| Active Directory Domain Services     | Provided centralized identity, authentication, and authorization   |
| Server Manager                       | Installed and managed Windows Server roles                         |
| Active Directory Users and Computers | Managed users, groups, computers, and OUs                          |
| DNS Manager                          | Managed and validated domain name resolution                       |
| Group Policy Management              | Configured and reviewed domain security policies                   |
| Windows Event Viewer                 | Reviewed authentication, account-management, and PowerShell events |
| PowerShell                           | Supported administration, testing, and validation                  |
| `gpupdate`                           | Forced Group Policy updates                                        |
| `gpresult`                           | Verified applied Group Policies                                    |
| Splunk Enterprise                    | Supported centralized security-event analysis                      |
| Wazuh                                | Supported endpoint monitoring and security-event visibility        |

## Security Skills Demonstrated

* Active Directory architecture, deployment, and administration
* Windows Server 2025 administration
* Domain-controller configuration
* Identity and access management
* User, group, and computer administration
* Organizational Unit design
* Role-based access management
* Privileged-account separation
* Service-account organization
* Principle of least privilege
* Active Directory-integrated DNS administration
* Group Policy administration
* Password and account-lockout policy management
* Windows domain hardening
* Endpoint security-policy enforcement
* Authentication and account-management auditing
* PowerShell security logging
* Windows security-event analysis
* SIEM and endpoint-monitoring preparation
* Technical validation and troubleshooting

## Project Results

The project established a functional and security-focused enterprise Windows domain with:

* Centralized authentication and authorization
* A structured Active Directory OU hierarchy
* Organized users, groups, computers, administrative accounts, and service accounts
* Role-based access through global security groups
* Separation of standard and privileged identities
* Active Directory-integrated DNS
* A successfully domain-joinedlk2011 Enterprise endpoint
* Centralized security-policy enforcement through Group Policy
* Password and account-lockout protections
* Authentication and PowerShell auditing
* Windows security-event visibility for investigations
* Integration readiness for Splunk and Wazuh

This environment provides the foundation for additional CyberLab projects involving failed-logon detection, account-lockout correlation, password-spray detection, privileged-account monitoring, incident investigation, and remediation.

## Evidence

The following sanitized evidence supports the project:

### Domain Controller Deployment

* Windows Server 2025 Server Manager showing `DC01`
* Active Directory Domain Services installation and domain-controller status

### Active Directory Configuration

* `cyberlab.local` displayed in Active Directory Users and Computers
* Organizational Unit hierarchy
* Sanitized user and security-group objects
* Computer, server, administrative-account, and service-account OUs

### Domain Membership

* `WIN11-CLIENT01` domain-membership confirmation
* Computer account displayed in Active Directory
* Sanitized `whoami` output confirming domain authentication

### Group Policy

* Group Policy Objects displayed in Group Policy Management
* Successful `gpupdate /force` output
* `gpresult` output confirming applied policies

### Security Auditing

* Authentication events displayed in Windows Event Viewer
* Account-management or account-lockout events
* PowerShell logging events, including event ID `4103` or `4104`
* Related event visibility in Splunk Enterprise or Wazuh

> **Evidence notice:** All screenshots must be sanitized before publication. Passwords, IP addresses, personal information, account identifiers, and unnecessary system or resource identifiers must be removed or obscured.

## Challenges and Resolutions

### DNS and Domain Connectivity

**Challenge:** Active Directory authentication and domain joining depend on correct DNS configuration.

**Resolution:** Configured the client workstation to use the domain controller’s DNS service and validated name resolution before joining it to the domain.

### Group Policy Application

**Challenge:** Newly configured policies did not always appear immediately on the domain-joined workstation.

**Resolution:** Used `gpupdate /force`, `gpresult /r`, and an HTML Group Policy report to refresh and validate policy application.

### Identity Organization

**Challenge:** Keeping identities and computers in default containers would make policy targeting and security administration difficult.

**Resolution:** Created a structured OU hierarchy for users, groups, computers, servers, administrative accounts, service accounts, and business departments.

### Privileged-Account Separation

**Challenge:** Using the same account for standard and administrative activities would increase security risk.

**Resolution:** Separated standard user accounts from privileged administrative accounts and placed them in dedicated OUs.

### Security-Event Visibility

**Challenge:** Default logging did not provide all the information required for detailed security investigations.

**Resolution:** Enabled authentication, account-management, and PowerShell auditing to improve visibility and prepare relevant events for centralized monitoring.

## Lessons Learned

* Active Directory depends heavily on correctly configured DNS.
* Static IP addressing supports reliable domain-controller operation.
* A well-designed OU structure improves policy targeting, security administration, and scalability.
* Security groups should assign access according to users’ responsibilities.
* Standard and privileged accounts should remain separate.
* Group Policy provides a consistent way to enforce domain and endpoint security settings.
* Security configurations must be tested and validated rather than assumed to be working.
* `gpupdate` and `gpresult` are essential Group Policy validation and troubleshooting tools.
* Authentication and PowerShell auditing improve detection and investigation capabilities.
* Centralized logging increases the security value of Windows events.
* Screenshots and command results provide stronger portfolio evidence than descriptions alone.
* Sensitive information must be sanitized before evidence is published publicly.

## Security and Privacy Statement

* All systems were created in an isolated and authorized CyberLab environment.
* No production systems or third-party accounts were accessed.
* All users, groups, systems, and security events were created for educational and portfolio purposes.
* Sensitive information is removed or obscured before screenshots are published.

## Related CyberLab Projects

* Windows Security Logging and Event Forwarding
* Splunk SIEM Deployment and Detection Engineering
* Wazuh SIEM and Endpoint Monitoring
* Failed Logon Detection
* Account Lockout Detection
* Password Spray Detection
* Privileged Account Monitoring
