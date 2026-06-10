# IAM User Setup for AWS CLI Access

## Overview

Before configuring AWS CLI, an AWS identity is required to authenticate API requests.

Although AWS provides a Root User for account administration, security best practices recommend using an IAM User for daily operations and AWS CLI access.

This document covers the process of creating an IAM User, generating access keys, and preparing credentials for AWS CLI authentication.

---

## Why Not Use the Root User?

The Root User has unrestricted access to all AWS resources and account settings.

Using the Root User for everyday administration increases security risks because:

* Full access to the AWS account
* Can modify billing settings
* Can delete resources
* Can close the AWS account
* Cannot be restricted using IAM policies

### AWS Best Practice

Use:

* Root User only for account-level tasks
* IAM Users for administration and daily operations
* IAM Roles for applications and services

---

## Understanding AWS CLI Authentication

AWS CLI authenticates using:

```text
Access Key ID
Secret Access Key
```

These credentials are associated with an IAM User.

```text
Local Machine
      |
      v
AWS CLI
      |
      v
Access Key + Secret Key
      |
      v
IAM User
      |
      v
AWS Services
```

---

## Objective

Create an IAM User that can securely access AWS through the AWS CLI.

---

## Step 1: Sign in as Root User

Log in to the AWS account using the Root User credentials.

Purpose:

* Initial account setup
* IAM User creation
* Security configuration

---

## Step 2: Open IAM Service

Navigate to:

```text
AWS Console → IAM
```

IAM (Identity and Access Management) is the AWS service used to manage users, groups, roles, and permissions.

---

## Step 3: Create an IAM User

Navigate to:

```text
IAM → Users → Create User
```

Example:

```text
aws-cli-admin
```

Provide a meaningful name that indicates the user's purpose.

---

## Step 4: Assign Permissions

For learning environments, attach:

```text
AdministratorAccess
```

Purpose:

* Full access to AWS resources
* Simplifies learning and experimentation

### Production Note

In production environments, permissions should follow the Principle of Least Privilege.

Only grant permissions required for specific tasks.

---

## Step 5: Create Access Keys

After creating the IAM User:

```text
IAM → Users → aws-cli-admin → Security Credentials
```

Select:

```text
Create Access Key
```

Choose:

```text
Command Line Interface (CLI)
```

AWS generates:

```text
Access Key ID
Secret Access Key
```

Example:

```text
Access Key ID     : AKIA*************
Secret Access Key : ************************
```

---

## Important Security Note

The Secret Access Key is displayed only once.

Store it securely.

If lost, AWS cannot recover it. A new access key must be generated.

Never:

* Commit keys to GitHub
* Share keys publicly
* Store keys in source code

---

## Where These Credentials Are Used

The generated credentials will later be configured using:

```bash
aws configure
```

Example:

```text
AWS Access Key ID: AKIA*************
AWS Secret Access Key: ************************
```

AWS CLI stores these credentials locally and uses them to authenticate API requests.

---

## Verification Strategy

After configuring AWS CLI, identity verification can be performed using:

```bash
aws sts get-caller-identity
```

Successful execution confirms:

* Credentials are valid
* IAM User permissions are working
* AWS CLI authentication is successful

---

## Observations

* AWS CLI requires IAM credentials to communicate with AWS.
* Root User credentials should not be used for daily administration.
* Access Keys function similarly to a username and password for API access.
* IAM provides secure and auditable access control.

---

## What I Learned

* Why AWS recommends IAM Users instead of the Root User.
* How AWS CLI authentication works.
* How Access Keys are generated and managed.
* The importance of securing AWS credentials.
* How IAM permissions control AWS CLI actions.

---

## Real-World Relevance

Cloud Engineers and DevOps Engineers commonly use IAM Users, IAM Roles, and temporary credentials to manage AWS environments securely.

Understanding IAM authentication is a foundational skill for:

* AWS Administration
* Infrastructure Automation
* CI/CD Pipelines
* DevOps Engineering
* Cloud Security

---

## Key Takeaways

* Created an IAM User for AWS CLI access.
* Generated Access Key ID and Secret Access Key.
* Followed AWS security best practices by avoiding Root User usage.
* Prepared credentials required for AWS CLI configuration.
* Established the foundation for secure AWS administration.
