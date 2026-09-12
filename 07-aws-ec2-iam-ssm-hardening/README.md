# AWS EC2 IAM & Systems Manager Hardening

## Project Overview

This project demonstrates secure administration of an Amazon EC2 workload using AWS Identity and Access Management and AWS Systems Manager Session Manager.

An Amazon Linux 2023 EC2 instance was configured with an IAM instance role and managed through a browser-based Session Manager connection. The instance security group contained zero inbound rules, eliminating the need to expose SSH port `22` or another public management port.

The project validates an identity-based and least-exposure approach to cloud workload administration.

## Project Status

✅ Completed

## Security Objectives

* Provision an Amazon EC2 workload
* Use an IAM role instead of long-term access keys
* Grant the instance the permissions required for Systems Manager
* Establish browser-based administrative access through Session Manager
* Eliminate inbound SSH access
* Configure the security group with zero inbound rules
* Validate the instance’s AWS identity
* Require Instance Metadata Service Version 2
* Verify instance and Systems Manager health
* Document the security controls with sanitized evidence

## AWS Environment

| Component              | Configuration                       |
| ---------------------- | ----------------------------------- |
| AWS Region             | US East (N. Virginia)               |
| EC2 Instance Name      | `AWS-CYBERLAB-SERVER01`             |
| Operating System       | Amazon Linux 2023                   |
| Architecture           | 64-bit x86                          |
| Instance Type          | `t3.micro`                          |
| Storage                | 8 GiB                               |
| Instance State         | Running                             |
| Status Checks          | 3/3 passed                          |
| Instance Metadata      | IMDSv2 required                     |
| IAM Role               | `EC2-CyberLab-SSM-Role`             |
| IAM Trust Principal    | `ec2.amazonaws.com`                 |
| IAM Permission Policy  | `AmazonSSMManagedInstanceCore`      |
| Role-Assumption Action | `sts:AssumeRole`                    |
| Administration Method  | AWS Systems Manager Session Manager |
| Security Group         | Zero inbound rules                  |
| SSH Exposure           | None                                |
| Identity Validation    | AWS Security Token Service          |

## Architecture and Access Flow

The secure-administration workflow consisted of:

1. An authorized administrator authenticated to AWS.
2. AWS Systems Manager initiated a browser-based Session Manager connection.
3. The EC2 instance used `EC2-CyberLab-SSM-Role` to authenticate to AWS services.
4. The `AmazonSSMManagedInstanceCore` policy provided the permissions required for Systems Manager communication.
5. The SSM agent established outbound communication with Systems Manager.
6. Session Manager provided shell access without opening inbound SSH.
7. AWS STS confirmed the role-based identity used by the EC2 instance.

## Implementation

### 1. EC2 Workload Provisioning

Provisioned an EC2 instance with the following configuration:

* Instance name: `AWS-CYBERLAB-SERVER01`
* Operating system: Amazon Linux 2023
* Architecture: 64-bit x86
* Instance type: `t3.micro`
* Storage: 8 GiB
* Region: US East (N. Virginia)
* Instance Metadata Service Version 2 required

After deployment, the instance was confirmed to be running with all three status checks passed.

### 2. IAM Role Creation

Created an IAM role named:

`EC2-CyberLab-SSM-Role`

The role was configured with:

| IAM Element                | Value                          |
| -------------------------- | ------------------------------ |
| Trusted AWS service        | EC2                            |
| Service principal          | `ec2.amazonaws.com`            |
| Trust action               | `sts:AssumeRole`               |
| Attached permission policy | `AmazonSSMManagedInstanceCore` |

The role enabled the EC2 workload to obtain temporary credentials and communicate with AWS Systems Manager without storing long-term access keys on the server.

### 3. IAM Role-Based Access

Associated the IAM role with the EC2 workload so that AWS permissions were delivered through temporary instance-role credentials.

This approach provided the following security advantages:

* No embedded AWS access keys
* No long-term credentials stored on the instance
* Automatic credential rotation
* Centralized permission management
* Reduced credential-exposure risk
* Easier permission revocation and auditing

### 4. Security Group Hardening

Configured the instance security group with:

* Zero inbound rules
* No inbound SSH rule
* No publicly exposed management port

This reduced the network attack surface because the instance did not accept unsolicited inbound management connections.

### 5. Systems Manager Configuration

Used AWS Systems Manager Session Manager to administer the EC2 instance.

The implementation included:

* Confirming that the required IAM permissions were available
* Verifying SSM agent connectivity
* Confirming that the managed node reported online or connected
* Starting a browser-based Session Manager session
* Accessing the instance shell without SSH
* Validating administrative connectivity without an inbound security-group rule

### 6. Instance Metadata Hardening

Configured the EC2 instance to require IMDSv2.

IMDSv2 improves protection of instance metadata and temporary role credentials by requiring session-oriented metadata requests.

### 7. AWS Identity Validation

Validated the AWS identity available to the EC2 workload using:

`aws sts get-caller-identity`

The command returned the active role-based identity and confirmed that the instance was using AWS temporary credentials associated with its IAM role.

The account ID, role-session information, and unnecessary identifiers were redacted before publication.

## Security Controls Implemented

| Security Control        | Implementation                   | Security Benefit                                       |
| ----------------------- | -------------------------------- | ------------------------------------------------------ |
| IAM instance role       | `EC2-CyberLab-SSM-Role`          | Replaced stored access keys with temporary credentials |
| Managed SSM permissions | `AmazonSSMManagedInstanceCore`   | Enabled authorized Systems Manager communication       |
| EC2 trust relationship  | `ec2.amazonaws.com`              | Limited role assumption to the EC2 service             |
| Session Manager         | Browser-based shell access       | Removed the need for inbound SSH                       |
| Zero inbound rules      | No inbound security-group access | Reduced the exposed network attack surface             |
| IMDSv2 required         | Session-oriented metadata access | Strengthened protection of instance metadata           |
| STS verification        | `get-caller-identity`            | Confirmed the active role-based identity               |
| Instance health checks  | 3/3 passed                       | Confirmed workload and AWS-system health               |

## Validation Activities

### EC2 Health Validation

* Confirmed that `AWS-CYBERLAB-SERVER01` was running
* Verified that all three EC2 status checks passed
* Confirmed the Amazon Linux 2023 operating system
* Verified the instance type and storage configuration
* Confirmed that IMDSv2 was required

### IAM Validation

* Confirmed the IAM role name
* Reviewed the EC2 trust relationship
* Verified the `ec2.amazonaws.com` service principal
* Confirmed the `sts:AssumeRole` trust action
* Verified the attached `AmazonSSMManagedInstanceCore` permission policy
* Confirmed that role-based credentials were available to the EC2 workload

### Systems Manager Validation

* Confirmed that the EC2 instance appeared as a managed node
* Verified that the SSM agent reported online or connected
* Started a browser-based Session Manager session
* Confirmed shell access to the Amazon Linux instance
* Verified that no SSH connection was required

### Network-Exposure Validation

* Reviewed the EC2 security group
* Confirmed that it contained zero inbound rules
* Confirmed that SSH port `22` was not exposed
* Verified that Session Manager access still functioned without inbound access

### Identity Validation

Executed:

`aws sts get-caller-identity`

Validation confirmed that:

* The instance could call AWS STS
* Authentication used the EC2 instance role
* Temporary role-based credentials were active
* Long-term access keys were not required for the validation

## Tools and AWS Services Used

| Tool or Service                | Purpose                                       |
| ------------------------------ | --------------------------------------------- |
| Amazon EC2                     | Hosted the Amazon Linux workload              |
| AWS IAM                        | Provided role-based authorization             |
| IAM Instance Role              | Delivered temporary AWS credentials to EC2    |
| `AmazonSSMManagedInstanceCore` | Granted core Systems Manager permissions      |
| AWS Systems Manager            | Managed the EC2 workload                      |
| Session Manager                | Provided browser-based shell access           |
| SSM Agent                      | Connected the EC2 instance to Systems Manager |
| Amazon EC2 Security Groups     | Controlled network access                     |
| AWS STS                        | Verified the active AWS identity              |
| IMDSv2                         | Protected instance metadata access            |
| AWS Management Console         | Supported provisioning and validation         |
| AWS CLI                        | Performed identity validation                 |

## Security Skills Demonstrated

* Amazon EC2 security
* AWS identity and access management
* IAM role creation
* IAM trust relationships
* Role-based access control
* Temporary credential use
* Least-exposure architecture
* Systems Manager administration
* Session Manager access
* SSM agent validation
* Security-group hardening
* SSH attack-surface reduction
* EC2 metadata protection
* AWS STS identity validation
* Cloud security testing
* Evidence sanitization
* Technical security documentation

## Project Results

The project successfully demonstrated:

* A functioning Amazon Linux 2023 EC2 workload
* A healthy EC2 instance with 3/3 status checks passed
* IAM role-based access through `EC2-CyberLab-SSM-Role`
* Systems Manager permissions through `AmazonSSMManagedInstanceCore`
* Temporary AWS credential use
* Successful Systems Manager enrollment
* An online and connected SSM agent
* Browser-based administrative access through Session Manager
* Zero inbound security-group rules
* No exposed SSH management port
* IMDSv2 enforcement
* Successful AWS identity validation through STS
* Sanitized documentation suitable for a public security portfolio

## Security Value

This configuration improves EC2 security by:

* Eliminating the need to expose SSH to the internet
* Reducing the instance’s inbound attack surface
* Avoiding long-term AWS credentials on the workload
* Using temporary role credentials
* Centralizing administrative access through AWS Systems Manager
* Strengthening instance-metadata protection
* Supporting auditable cloud administration
* Providing a repeatable model for securely managing cloud workloads

## Evidence

The following sanitized evidence supports the completed exercise:

### IAM Role

* IAM role `EC2-CyberLab-SSM-Role`
* EC2 service trust relationship
* `AmazonSSMManagedInstanceCore` attached permission policy

### EC2 Workload

* `AWS-CYBERLAB-SERVER01` in the Running state
* Amazon Linux 2023 configuration
* 3/3 EC2 status checks passed
* IMDSv2 displayed as required

### Systems Manager

* EC2 instance displayed as a managed node
* SSM agent status displayed as online or connected
* Successful browser-based Session Manager connection
* Terminal access without SSH

### Security Group

* Security group displaying zero inbound rules
* No inbound rule for TCP port `22`
* Instance remaining manageable through Session Manager

### AWS Identity

* Successful `aws sts get-caller-identity` output
* Role-based identity associated with the EC2 workload
* Redacted AWS account and session identifiers

> **Evidence notice:** AWS account IDs, role-session identifiers, public IP addresses, instance IDs, unnecessary resource identifiers, and other sensitive information must be removed or obscured before screenshots are published.

## Challenges and Resolutions

### Systems Manager Initially Unavailable

**Challenge:** Session Manager access depends on the IAM role, permission policy, SSM agent, network connectivity, and Systems Manager registration.

**Resolution:** Verified the EC2 trust relationship, confirmed the `AmazonSSMManagedInstanceCore` policy, checked the SSM agent, and confirmed that the instance appeared online in Systems Manager.

### Secure Access Without SSH

**Challenge:** Traditional EC2 administration commonly depends on SSH and an inbound port.

**Resolution:** Used Systems Manager Session Manager to establish a browser-based shell while keeping the security group free of inbound rules.

### Identity Confirmation

**Challenge:** Administrative access alone did not prove which AWS identity the workload was using.

**Resolution:** Executed `aws sts get-caller-identity` from the instance and confirmed the role-based identity.

### Public Evidence Sanitization

**Challenge:** AWS console screenshots and command output can expose account, session, address, and resource identifiers.

**Resolution:** Redacted sensitive identifiers while preserving the configuration details required to demonstrate the security control.

## Lessons Learned

* IAM roles are safer than storing long-term access keys on EC2 instances.
* Systems Manager Session Manager can provide administrative access without exposing SSH.
* Security groups should permit only required network access.
* An EC2 instance can remain manageable with zero inbound rules.
* SSM access depends on working IAM permissions, agent health, and AWS service connectivity.
* STS provides a direct method for validating the active AWS identity.
* IMDSv2 strengthens protection of instance metadata and temporary credentials.
* Instance and Systems Manager health should be validated separately.
* Secure configuration should be supported by technical evidence.
* AWS screenshots must be sanitized carefully before public release.

## Security and Privacy Statement

* All activities were performed in an authorized AWS CyberLab account.
* No production workloads or third-party systems were accessed.
* No passwords, private keys, or long-term AWS access keys are included in this repository.
* Sensitive account, session, address, and resource identifiers are removed or obscured.
* The project demonstrates defensive cloud-security administration for educational and portfolio purposes.

## Related CyberLab Projects

* AWS CloudTrail and CloudWatch Alerting
* AWS IAM Least-Privilege Validation
* AWS Security Monitoring
* Cloud Misconfiguration Detection
* Infrastructure-as-Code Security
* DevSecOps Pipeline Security
