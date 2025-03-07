---
title: "Audit Logs"
metaTitle: "Spectro Cloud user audit logs"
metaDescription: "Spectro Cloud logs for every event occurring under a user for every Kubernetes cluster"
icon: "admin"
hideToC: false
fullWidth: false
---

import WarningBox from 'shared/components/WarningBox';

# About Audit Logs

The Spectro Cloud management platform application captures audit logs to track the user interaction with the application resources along with the timeline. For certain resources, the system-level modifications are also captured in the audit logs.

The audit log contains information about the resource and the user who performed the action. The user or the system action on the resource is classified as *Create*, *Update*, and *Delete*. Every resource is categorized as a type that helps the user to scope down the audit logs.

Audit logs are retained for the last 1 year.

# Accessing Audit Logs

Audits can be accessed for the tenant scope and the project scope. The tenant scope audits show all the activity logs across all projects and tenant actions. The project scope audits show the activity logs for the specific project.

* The tenant scope audit logs can be accessed in the Spectro Cloud console under the **Admin > Audit Logs**. The user should have the *Tenant Admin* role or at least the `audit.get` and `audit.list` permissions at the tenant scope to access the audit logs.
* The project scope audit logs can be accessed under the **Project** *selection* > **Audit Logs**. The user should have at least the *Project Viewer* role with `audit.get` and `audit.list` permissions for the selected project to access the audit logs.
* Tenant admins (or users with appropriate permissions) can download the audit logs as a *.csv file.

# Filtering Audit Logs

The audit logs can be filtered based on user and resource attributes. The following attributes can be used to filter the audit logs:

* Type - The action type on the resource.
* Resource Type - The resource type. (The resources are grouped based on the type).
* Start Date and End Date - Period range for the audit logs.

# Adding Update Note

For certain resources like the Cluster Profile, users can associate a custom update note in addition to the generic audit event log. On a successful save of the Cluster Profile, the user will be prompted to provide an update note about the changes made on the profile. This message will be shown when the user selects an audit log from the list.

# Pushing the Audit Log to the AWS Cloud Trail

Spectro Cloud users can now push the compliance, management, operational, and risk audit logs to the AWS CloudTrail. This enables continuous monitoring, security analysis, resource tracking, and troubleshooting of the workload cluster using the event history.

<WarningBox>
An AWS account with cloud trail created is the prerequisite.

The permissions listed need to be enabled for CloudWatch.
</WarningBox>

## Permission List

Ensure that the IAM user or the ROOT user role created should have the following IAM policy included for Amazon CloudWatch:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:DescribeLogGroups",
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "logs:DeleteLogStream",
        "logs:DescribeLogStreams"
      ],
      "Resource": [
        "<CLOUDWATCH-LOG-GROUP-ARN>;"
      ]
    }
  ]
}
```
## Instructions to Push Cluster Audit Logs to AWS Trails 

* Go to Admin Settings and select Audit Trails.
* Select the wizard ‘Add new Audit Trail’ and fill in the following details:

  * Audit Name: Custom name to identify the logs
  * Type: Choice of monitoring service (currently set to AWS Cloud Watch)
  * Group: The log group name obtained from cloud watch logs of AWS cloud trail creation
  * Region: The region of the AWS account
  * Method of verification:
   	* Credentials:
Use the AWS Access Key and Secret Access Key to validate the AWS account for pushing the Audit log trails from Spectro Cloud console.
   	* STS:
Use Amazon’s unique resource identifier- ARN, to validate the AWS account for pushing the Audit log trails from Spectro Cloud console.
	
* Stream Optional.
* Confirm the information to complete the audit trail creation wizard.
* The audit trail could be edited and deleted using the kebab menu.


