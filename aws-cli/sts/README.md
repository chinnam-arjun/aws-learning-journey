# AWS Security Token Service (STS)

## Overview

AWS Security Token Service (STS) is a service that provides information about the identity currently being used to access AWS resources and enables the creation of temporary security credentials.

In day-to-day AWS CLI operations, STS is commonly used to verify which AWS account, IAM user, or IAM role is currently authenticated before performing administrative actions.

This document focuses on identity verification using AWS CLI and explores how STS helps cloud engineers avoid mistakes when working across multiple AWS accounts and environments.

---

## What is AWS STS?

AWS STS stands for:

```text id="mn9p95"
Security Token Service
```

STS is responsible for:

* Identity verification
* Temporary credentials
* Role assumption
* Cross-account access
* Federated access

For this lab, the primary focus is:

```text id="w79lnq"
aws sts get-caller-identity
```

which helps determine the identity currently authenticated with AWS CLI.

---

## Why STS is Important

Before performing cloud administration tasks, engineers often verify:

* Which AWS account is active
* Which IAM User is authenticated
* Which IAM Role is being used
* Which AWS profile is currently active

This reduces the risk of accidentally modifying resources in the wrong AWS account.

---

## STS Identity Verification

Command:

```bash id="gpdzjl"
aws sts get-caller-identity
```

Example Output:

```json id="s7g7ml"
{
  "UserId": "********",
  "Account": "************",
  "Arn": "arn:aws:iam::************:user/aws-cli-admin"
}
```


---

## Understanding the Output

### UserId

Represents the authenticated IAM identity.

Example:

```text id="lkh2gk"
AIDA**************
```

---

### Account

Represents the AWS Account ID.

Example:

```text id="6b7v2o"
123456789012
```

---

### ARN

ARN stands for:

```text id="y8ycvj"
Amazon Resource Name
```

Example:

```text id="59qd2m"
arn:aws:iam::123456789012:user/aws-cli-admin
```

The ARN uniquely identifies the AWS resource or identity.

---

## Verifying Different Profiles

If multiple profiles exist, STS can verify each profile independently.

### Development Profile

```bash id="i4gqgl"
aws sts get-caller-identity --profile dev
```

---

### Production Profile

```bash id="k9g2sy"
aws sts get-caller-identity --profile prod
```

This helps confirm which AWS account is associated with each profile.

---

## Exploring Output Formats

AWS CLI supports multiple output formats.

### Table Output

Command:

```bash id="z5rj2g"
aws sts get-caller-identity --output table
```


---

### JSON Output

Command:

```bash id="q95zd8"
aws sts get-caller-identity --output json
```

---

### Text Output

Command:

```bash id="47swn7"
aws sts get-caller-identity --output text
```


---

## Querying Specific Information

AWS CLI supports filtering output using queries.

### Retrieve Account ID

```bash id="wibncz"
aws sts get-caller-identity --query Account
```

---

### Retrieve ARN

```bash id="0kj7wn"
aws sts get-caller-identity --query Arn
```


---

### Retrieve User ID

```bash id="67g4y5"
aws sts get-caller-identity --query UserId
```

---

## Execution Process

### Step 1

Verify current AWS identity.

```bash id="l9h2j4"
aws sts get-caller-identity
```

### Step 2

Verify identities associated with different profiles.

```bash id="7yv5ff"
aws sts get-caller-identity --profile dev

aws sts get-caller-identity --profile prod
```

### Step 3

Experiment with output formats.

```bash id="4mmt3g"
aws sts get-caller-identity --output table

aws sts get-caller-identity --output json

aws sts get-caller-identity --output text
```

### Step 4

Extract specific information using queries.

```bash id="l77cif"
aws sts get-caller-identity --query Account

aws sts get-caller-identity --query Arn

aws sts get-caller-identity --query UserId
```

---

## Commands Practiced

```bash id="bkk7ea"
aws sts get-caller-identity

aws sts get-caller-identity --profile dev

aws sts get-caller-identity --profile prod

aws sts get-caller-identity --output table

aws sts get-caller-identity --output json

aws sts get-caller-identity --output text

aws sts get-caller-identity --query Account

aws sts get-caller-identity --query Arn

aws sts get-caller-identity --query UserId
```

---

## Observations

* STS is one of the quickest methods to verify AWS CLI authentication.
* Profile verification helps prevent operations in the wrong AWS account.
* Output formatting improves readability.
* Querying allows extraction of specific values from AWS CLI responses.
* STS does not require additional IAM permissions in most standard configurations.

---

## What I Learned

* What AWS Security Token Service (STS) is.
* How to verify active AWS identities.
* How to identify the AWS account currently in use.
* How to verify profile-specific identities.
* How to use output formats and queries with AWS CLI.

---

## Real-World Relevance

Cloud Engineers and DevOps Engineers frequently execute:

```bash id="1ecb7s"
aws sts get-caller-identity
```

before:

* Creating infrastructure
* Modifying production resources
* Running automation scripts
* Troubleshooting AWS environments

It is a simple but critical verification step that helps prevent costly mistakes.

---

## Key Takeaways

* STS provides identity verification capabilities.
* `get-caller-identity` confirms the active AWS user, role, or account.
* Profile-based verification helps manage multiple AWS environments safely.
* Output formatting and querying improve command usability.
* STS is an essential AWS CLI troubleshooting and verification tool.
