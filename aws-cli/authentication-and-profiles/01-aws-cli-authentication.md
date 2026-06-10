# AWS CLI Authentication

## Overview

Before AWS CLI can interact with AWS services, it must authenticate every request sent to AWS APIs.

Authentication is the process of proving the identity of the user making the request. AWS CLI uses credentials associated with an IAM User to authenticate and authorize access to AWS resources.

This document explores how AWS CLI authentication works, where credentials are stored, and how to verify successful authentication.

---

## Why Authentication is Required

AWS resources contain sensitive data and infrastructure components that cannot be accessed anonymously.

When a command is executed, AWS must verify:

* Who is making the request
* Whether the credentials are valid
* Whether the user has permission to perform the action

Example:

```bash
aws ec2 describe-instances
```

Before returning information, AWS validates the identity and permissions of the requester.

---

## Authentication Components

AWS CLI primarily uses two credentials:

```text
Access Key ID
Secret Access Key
```

These credentials are generated from an IAM User and act as the identity used by AWS CLI.

Example:

```text
IAM User
   │
   ├── Access Key ID
   └── Secret Access Key
```

---

## Authentication Flow

```text
Local Machine
      │
      ▼
AWS CLI Command
      │
      ▼
Credentials
(Access Key + Secret Key)
      │
      ▼
AWS IAM Validation
      │
      ▼
Permission Check
      │
      ▼
AWS Service API
      │
      ▼
Response
```

---

## Obtaining Credentials

Credentials are generated from an IAM User.

### Navigation

```text
AWS Console
  └── IAM
      └── Users
          └── Select User
              └── Security Credentials
                  └── Create Access Key
```

### Screenshot

```text
screenshots/01-create-access-key.png
```

AWS generates:

```text
Access Key ID
Secret Access Key
```

> Never expose these credentials publicly.

---

## Configuring AWS CLI Authentication

Configure credentials using:

```bash
aws configure
```

CLI prompts:

```text
AWS Access Key ID:
AWS Secret Access Key:
Default region name:
Default output format:
```

Example:

```text
AWS Access Key ID: ****************
AWS Secret Access Key: ****************
Default region name: ap-south-1
Default output format: json
```

### Screenshot

```text
screenshots/02-aws-configure.png
```

---

## Viewing Current Configuration

To view the current AWS CLI configuration:

```bash
aws configure list
```

Example Output:

```text
Name                    Value
----                    -----
profile                 <not set>
access_key              ************
secret_key              ************
region                  ap-south-1
```

### Screenshot

```text
screenshots/03-configure-list.png
```

---

## Where AWS CLI Stores Credentials

AWS CLI stores configuration locally on the machine.

### Credentials File

Location:

```text
~/.aws/credentials
```

Example:

```ini
[default]
aws_access_key_id=XXXXXXXXXXXX
aws_secret_access_key=XXXXXXXXXXXX
```

### Screenshot

```text
screenshots/04-credentials-file.png
```

---

### Configuration File

Location:

```text
~/.aws/config
```

Example:

```ini
[default]
region=ap-south-1
output=json
```

### Screenshot

```text
screenshots/05-config-file.png
```

---

## Verifying Authentication

Once configured, verify the active identity.

Command:

```bash
aws sts get-caller-identity
```

Example Output:

```json
{
  "UserId": "********",
  "Account": "********",
  "Arn": "arn:aws:iam::********:user/aws-cli-admin"
}
```

### Screenshot

```text
screenshots/06-sts-verification.png
```

This confirms:

* Credentials are valid
* AWS CLI can communicate with AWS
* Authentication is successful

---

## Common Authentication Errors

### Unable to Locate Credentials

Example:

```text
Unable to locate credentials
```

Cause:

* AWS CLI not configured
* Missing credentials file

Resolution:

```bash
aws configure
```

---

### InvalidClientTokenId

Example:

```text
The security token included in the request is invalid.
```

Cause:

* Incorrect Access Key
* Deleted credentials

Resolution:

* Generate new credentials
* Reconfigure AWS CLI

---

### AccessDenied

Example:

```text
AccessDenied
```

Cause:

* IAM User lacks required permissions

Resolution:

* Review IAM policies
* Grant necessary permissions

---

## Security Best Practices

### Use IAM Users

Avoid using Root User credentials for AWS CLI operations.

### Protect Access Keys

Never:

* Upload credentials to GitHub
* Store credentials in source code
* Share credentials publicly

### Enable MFA

Use Multi-Factor Authentication for privileged accounts.

### Rotate Keys

Regularly replace Access Keys to reduce security risks.

---

## Observations

* Every AWS CLI request requires authentication.
* Authentication occurs before authorization.
* AWS CLI stores credentials locally.
* Invalid credentials immediately prevent API access.
* STS verification is useful for confirming identity.

---

## What I Learned

* How AWS CLI authenticates requests.
* The purpose of Access Key ID and Secret Access Key.
* Where AWS CLI stores credentials.
* How to verify authentication using STS.
* Common authentication issues and resolutions.

---

## Real-World Relevance

Authentication is the foundation of all AWS operations.

It is used in:

* Cloud Administration
* Infrastructure Automation
* CI/CD Pipelines
* Monitoring Systems
* DevOps Workflows
* Infrastructure as Code

Without proper authentication, AWS resources cannot be managed securely.

---

## Commands Practiced

```bash

aws --version

aws configure

aws configure list

cat ~/.aws/credentials
# or Get-Content $HOME\.aws\credentials

cat ~/.aws/config
# or Get-Content $HOME\.aws\config

aws sts get-caller-identity

aws configure get region

aws configure get output
```

---

## Key Takeaways

* AWS CLI authenticates using IAM credentials.
* Access Key ID and Secret Access Key identify and authenticate users.
* Credentials are stored locally within the `.aws` directory.
* STS helps verify the active AWS identity.
* Secure credential management is critical for cloud security.
