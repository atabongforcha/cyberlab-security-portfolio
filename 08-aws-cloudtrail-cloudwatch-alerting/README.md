# AWS CloudTrail & CloudWatch Security Alerting

## Project Overview

This project demonstrates the implementation and validation of a foundational AWS security-monitoring and alerting workflow using AWS CloudTrail, Amazon CloudWatch, and Amazon Simple Notification Service.

CloudTrail activity logs were integrated with CloudWatch monitoring. A metric-based alarm was configured to identify suspicious AWS API activity and publish an email notification through Amazon SNS. The project also documented the associated investigation process, security rationale, and remediation guidance.

## Project Status

✅ Completed

> This README documents the completed CloudTrail, CloudWatch, metric-alarm, and email-notification exercise. The broader AWS Security Monitoring program—including Amazon GuardDuty and AWS Security Hub—remains in progress.

## Project Objectives

* Enable AWS API activity logging with CloudTrail
* Provide centralized visibility into AWS account activity
* Integrate CloudTrail events with CloudWatch Logs
* Define metric-based detection for suspicious API activity
* Configure a CloudWatch alarm
* Create an Amazon SNS notification workflow
* Confirm the email subscription
* Validate security-notification delivery
* Document an analyst investigation process
* Define appropriate remediation guidance
* Preserve sanitized technical evidence

## AWS Services Used

| AWS Service              | Purpose                                                 |
| ------------------------ | ------------------------------------------------------- |
| AWS CloudTrail           | Recorded AWS API and account activity                   |
| Amazon CloudWatch Logs   | Centralized CloudTrail log events                       |
| CloudWatch Metric Filter | Converted matching log activity into a security metric  |
| CloudWatch Alarm         | Evaluated the metric and triggered notification actions |
| Amazon SNS               | Distributed the security notification                   |
| Email Subscription       | Delivered the alert to the designated recipient         |
| AWS IAM                  | Supported service permissions and access control        |
| AWS Management Console   | Supported configuration, monitoring, and validation     |

## Monitoring Architecture

The completed monitoring workflow consisted of:

1. An AWS API or account activity occurred.
2. AWS CloudTrail recorded the activity.
3. The CloudTrail event was delivered to CloudWatch Logs.
4. A metric filter evaluated the event against the configured security-detection pattern.
5. Matching activity increased the associated CloudWatch metric.
6. The CloudWatch alarm evaluated the metric.
7. The alarm published a notification to Amazon SNS.
8. Amazon SNS delivered the security notification by email.
9. The event could then be reviewed for investigation and remediation.

## Implementation

### 1. CloudTrail Activity Logging

Configured AWS CloudTrail to provide visibility into AWS account and API activity.

CloudTrail records useful investigative information such as:

* Event time
* Event source
* Event name
* AWS Region
* User identity
* Source IP address
* User agent
* Request parameters
* Response elements
* Error code and error message
* Affected AWS resources

This information supports security monitoring, incident investigation, change tracking, and audit activities.

### 2. CloudWatch Logs Integration

Integrated CloudTrail activity with Amazon CloudWatch Logs.

This integration enabled:

* Centralized searching of CloudTrail activity
* Near-real-time evaluation of relevant log events
* Metric creation from matching event patterns
* Alarm generation
* Automated notification through Amazon SNS

### 3. Metric-Based Detection

Created a CloudWatch Logs metric filter for suspicious AWS API activity.

The metric filter was designed to:

* Evaluate incoming CloudTrail events
* Match the configured suspicious-activity pattern
* Publish a metric value when matching activity occurred
* Provide a measurable signal for the CloudWatch alarm

The exact production value of the detection depends on the event pattern, threshold, time window, and expected baseline for the AWS environment.

### 4. CloudWatch Alarm Configuration

Created a CloudWatch alarm based on the security metric.

The alarm configuration included:

* Selection of the security metric
* Definition of the evaluation criteria
* Configuration of the threshold
* Selection of the evaluation period
* Configuration of missing-data behavior
* Association of the alarm with an SNS notification action
* Review of alarm state and history

The alarm converted matching log activity into an actionable security signal.

### 5. Amazon SNS Notification

Configured Amazon SNS to distribute CloudWatch alarm notifications.

The notification workflow included:

* Creating or selecting an SNS topic
* Adding an email subscription
* Confirming the subscription from the recipient’s email
* Associating the SNS topic with the CloudWatch alarm
* Validating that the notification workflow was active

An SNS email subscription remains unable to receive alarm messages until the recipient confirms it.

### 6. Alert Validation

Validated the monitoring workflow by confirming that:

* CloudTrail recorded AWS activity
* CloudTrail events were available to CloudWatch Logs
* The metric filter evaluated matching activity
* The security metric received data
* The CloudWatch alarm evaluated the metric
* The alarm action referenced the correct SNS topic
* The email subscription was confirmed
* A security notification was delivered through the configured workflow

### 7. Evidence Sanitization

Reviewed screenshots and command output before publication.

The following information was removed or obscured where necessary:

* AWS account IDs
* Session identifiers
* Source or public IP addresses
* Email addresses
* Resource ARNs
* Trail identifiers
* Log-group identifiers
* SNS topic identifiers
* CloudWatch alarm identifiers
* Unnecessary resource IDs

## Validation Activities

### CloudTrail Validation

* Verified that CloudTrail activity logging was enabled
* Reviewed recent AWS API activity
* Confirmed that events contained timestamps, event names, and identity context
* Verified that the expected activity was available for investigation

### CloudWatch Logs Validation

* Confirmed that CloudTrail events were delivered to CloudWatch Logs
* Reviewed log events within the applicable time range
* Verified that relevant API activity was searchable
* Confirmed that the event structure supported metric filtering

### Metric Filter Validation

* Reviewed the metric-filter pattern
* Confirmed that the filter was associated with the correct log group
* Verified that matching activity produced metric data
* Confirmed that the metric was available to CloudWatch alarms

### CloudWatch Alarm Validation

* Reviewed the alarm threshold and evaluation configuration
* Confirmed the alarm’s notification action
* Reviewed the alarm state and alarm history
* Verified that the alarm responded to the security metric
* Confirmed that missing-data behavior was configured intentionally

### SNS Validation

* Verified the SNS topic
* Confirmed the email subscription
* Confirmed that the subscription was no longer pending
* Verified that the topic was associated with the CloudWatch alarm
* Confirmed email-notification delivery

### End-to-End Validation

The complete workflow was validated from event generation through notification:

* AWS activity recorded by CloudTrail
* Event delivered to CloudWatch Logs
* Event matched by the metric filter
* Metric evaluated by the CloudWatch alarm
* Alarm notification published to SNS
* Email notification delivered to the confirmed recipient

## Investigation Workflow

When the alarm generates a notification, the analyst should:

1. Record the alarm name, state, timestamp, and reason.
2. Review the corresponding CloudWatch log events.
3. Locate the relevant CloudTrail event.
4. Identify the event name and AWS service.
5. Review the user identity and session context.
6. Determine whether the activity came from a user, assumed role, or AWS service.
7. Review the source IP address and user agent.
8. Identify the affected resource.
9. Review request parameters and response details.
10. Determine whether the activity was authorized.
11. Search for related events by the same identity, address, session, or resource.
12. Document the findings and response actions.

## Security Analysis

### Potential Indicators of Suspicious Activity

* Unexpected API activity
* Activity performed by an unfamiliar identity
* Administrative actions outside the expected change window
* Requests from an unfamiliar source address
* Repeated denied API requests
* Changes to logging, monitoring, IAM, or security controls
* Activity involving sensitive resources
* Actions inconsistent with the identity’s normal responsibilities

### Potential Benign Causes

* Authorized administrative activity
* A planned configuration change
* Automated deployment activity
* A legitimate service or scheduled operation
* Testing performed as part of the CyberLab
* Incorrectly tuned detection criteria

The alarm should be treated as an investigative signal rather than automatic proof of compromise.

## Remediation Guidance

Depending on the investigation results, appropriate actions may include:

* Validate the activity with the responsible administrator
* Disable or restrict a suspected IAM principal
* Revoke active sessions
* Rotate exposed credentials
* Remove unnecessary permissions
* Update the affected IAM policy
* Revert unauthorized resource changes
* Restrict network access
* Restore modified monitoring controls
* Preserve CloudTrail evidence
* Review related API activity
* Adjust the detection threshold or filter when a benign pattern is confirmed
* Document the incident and corrective actions

## Security Controls Demonstrated

| Security Control           | Implementation             | Security Benefit                              |
| -------------------------- | -------------------------- | --------------------------------------------- |
| API audit logging          | AWS CloudTrail             | Created a record of AWS activity              |
| Centralized log monitoring | CloudWatch Logs            | Enabled event searching and evaluation        |
| Metric-based detection     | CloudWatch metric filter   | Converted log matches into measurable signals |
| Automated alerting         | CloudWatch alarm           | Identified matching activity requiring review |
| Notification workflow      | Amazon SNS                 | Distributed security notifications            |
| Email delivery             | Confirmed SNS subscription | Delivered alerts to a monitored inbox         |
| Investigation process      | CloudTrail event analysis  | Supported identity and activity attribution   |
| Evidence protection        | Identifier redaction       | Reduced exposure of sensitive AWS information |

## Tools and Technologies Used

| Tool or Technology        | Purpose                                   |
| ------------------------- | ----------------------------------------- |
| AWS CloudTrail            | API activity logging and investigation    |
| Amazon CloudWatch Logs    | Centralized CloudTrail event monitoring   |
| CloudWatch Metric Filters | Security-event pattern matching           |
| CloudWatch Metrics        | Measurement of matching activity          |
| CloudWatch Alarms         | Threshold evaluation and alert generation |
| Amazon SNS                | Notification distribution                 |
| Email                     | Receipt of security alerts                |
| AWS IAM                   | Access control and service integration    |
| AWS Management Console    | Configuration and validation              |

## Security Skills Demonstrated

* AWS security monitoring
* CloudTrail configuration and analysis
* CloudWatch Logs administration
* Log-based detection engineering
* Metric-filter configuration
* CloudWatch alarm configuration
* Amazon SNS integration
* Security-notification validation
* AWS API activity investigation
* IAM identity analysis
* Cloud incident triage
* Alert tuning
* Remediation planning
* Evidence collection and sanitization
* Technical security documentation

## Project Results

The project successfully demonstrated:

* AWS API activity logging through CloudTrail
* CloudTrail integration with CloudWatch Logs
* Metric-based monitoring of suspicious AWS API activity
* CloudWatch alarm configuration
* Amazon SNS email integration
* Email-subscription confirmation
* End-to-end security-notification delivery
* A repeatable alert-investigation workflow
* Documented remediation guidance
* Sanitized evidence suitable for a public security portfolio

## Security Value

This project demonstrates how native AWS services can create a foundational cloud detection-and-alerting workflow.

The implementation supports:

* Visibility into AWS account activity
* Rapid identification of selected suspicious API activity
* Automated notification
* Identity and session analysis
* Cloud-change investigation
* Audit and compliance support
* Incident triage and remediation
* Future integration with GuardDuty and Security Hub

## Evidence

The following sanitized evidence should support the completed project:

### CloudTrail Evidence

* CloudTrail activity logging enabled
* Recent API activity visible in Event history or the configured logging destination
* Event details showing the event name, time, service, and identity context

### CloudWatch Logs Evidence

* CloudTrail events visible in CloudWatch Logs
* Relevant event details displayed within the selected time range
* Metric filter associated with the correct log group

### Metric and Alarm Evidence

* Security metric configuration
* CloudWatch alarm threshold and evaluation settings
* Alarm notification action
* Alarm state or alarm history
* Configured missing-data treatment

### SNS Evidence

* SNS topic associated with the alarm
* Email subscription displayed as confirmed
* Delivered security-notification email

### Investigation Evidence

* Relevant CloudTrail event
* Identity and session context
* Source information
* Affected AWS service or resource
* Sanitized investigation notes and remediation guidance

> **Evidence notice:** AWS account IDs, session identifiers, IP addresses, email addresses, ARNs, resource IDs, trail names, log-group names, alarm names, and SNS topic details must be removed or obscured when they are not necessary to demonstrate the security control.

## Challenges and Resolutions

### Email Notification Not Initially Received

**Challenge:** The alert email was not received while the SNS email subscription was awaiting confirmation or while the alarm workflow was being validated.

**Resolution:** Verified the destination address, located the SNS subscription confirmation message, confirmed the subscription, reviewed the alarm action, and validated notification delivery.

### Missing or Delayed Metric Data

**Challenge:** A metric filter only produces data when incoming log events match the configured pattern.

**Resolution:** Confirmed CloudTrail delivery to CloudWatch Logs, reviewed the metric-filter pattern and time range, and generated or identified matching activity for validation.

### Alarm Missing-Data Behavior

**Challenge:** Periods without matching security events could affect how the alarm evaluated the metric.

**Resolution:** Selected the missing-data treatment deliberately based on the behavior expected from the security metric and reviewed its effect during validation.

### Limited Context in the Notification

**Challenge:** An alarm notification signals that a condition occurred but may not include all information required to determine intent.

**Resolution:** Used the alarm timestamp and reason to locate the corresponding CloudWatch and CloudTrail events, then reviewed the identity, source, request, and affected resource.

### Sensitive Information in AWS Evidence

**Challenge:** AWS console screenshots and log events can expose account, session, address, email, and resource identifiers.

**Resolution:** Redacted sensitive information while retaining the technical fields required to demonstrate configuration and validation.

## Lessons Learned

* CloudTrail provides the foundational record for investigating AWS API activity.
* CloudWatch Logs enables automated analysis of CloudTrail events.
* Metric filters convert matching log activity into measurable security signals.
* CloudWatch alarms require carefully selected thresholds and evaluation settings.
* Missing-data treatment should be configured intentionally.
* SNS email subscriptions must be confirmed before notifications can be delivered.
* An alert is an investigative starting point, not automatic proof of compromise.
* Identity, source, timestamp, request, and resource context are essential during investigation.
* End-to-end testing is required to prove that the complete notification pipeline works.
* Screenshots and logs must be sanitized before public publication.
* Native AWS services can provide an effective foundation for cloud detection engineering.

## Current Scope and Next Steps

This completed exercise covers CloudTrail logging, CloudWatch monitoring, metric-based alerting, Amazon SNS, and email notification.

The broader AWS Security Monitoring program remains in progress. Planned extensions include:

* Amazon GuardDuty
* AWS Security Hub
* Additional suspicious API detections
* Expanded IAM monitoring
* Formal alert severity classification
* Additional investigation playbooks
* Centralized multi-account monitoring

## Security and Privacy Statement

* All activities were performed in an authorized AWS CyberLab account.
* No production workloads or third-party systems were accessed.
* Test activity was used to validate the monitoring workflow.
* No access keys, passwords, or confidential data are included.
* Sensitive AWS identifiers are removed or obscured before publication.

## Related CyberLab Projects

* AWS EC2 IAM and Systems Manager Hardening
* AWS IAM Least-Privilege Validation
* AWS Security Monitoring
* Amazon GuardDuty Detection
* AWS Security Hub Integration
* Cloud Misconfiguration Detection
* Cloud Incident Investigation
