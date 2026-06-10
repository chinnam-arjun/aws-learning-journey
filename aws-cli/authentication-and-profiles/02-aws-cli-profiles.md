# AWS CLI Profiles

## Overview

As cloud environments grow, engineers often need to work with multiple AWS accounts and environments.

Examples:

```text
Personal AWS Account
Development Account
Testing Account
Production Account
Client Accounts
```

AWS CLI Profiles allow multiple configurations to be stored on a single machine and enable switching between them without repeatedly reconfiguring credentials.

This document explores how AWS CLI profiles work and how they simplify multi-account administration.

---

## What is a Profile?

A profile is a named AWS CLI configuration that contains:

* Access Key ID
* Secret Access Key
* Default Region
* Output Format

Example:

```text
default
dev
test
prod
```

Each profile can connect to a different AWS account or environment.

---

## Why Profiles are Needed

Without profiles:

```text
AWS Account A
      ↓
aws configure

Need AWS Account B
      ↓
Run aws configure again
      ↓
Overwrite Account A credentials
```

This becomes difficult to manage.

Profiles solve this problem.

```text
default → Personal Lab
dev     → Development Environment
test    → Testing Environment
prod    → Production Environment
```

---

## Viewing Existing Profiles

Command:

```bash
aws configure list-profiles
```

Example Output:

```text
default
dev
prod
```

### Screenshot

```text
screenshots/01-list-profiles.png
```

---

## Creating a New Profile

### Create Development Profile

Command:

```bash
aws configure --profile dev
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
Profile Name : dev
Region       : ap-south-1
Output       : json
```

### Screenshot

```text
screenshots/02-create-dev-profile.png
```

---

## Creating a Production Profile

Command:

```bash
aws configure --profile prod
```

Example:

```text
Profile Name : prod
Region       : us-east-1
Output       : json
```

### Screenshot

```text
screenshots/03-create-prod-profile.png
```

---

## Profile Storage Location

Profiles are stored within:

### Credentials File

```text
~/.aws/credentials
```

Example:

```ini
[default]
aws_access_key_id=XXXXXXXX
aws_secret_access_key=XXXXXXXX

[dev]
aws_access_key_id=XXXXXXXX
aws_secret_access_key=XXXXXXXX

[prod]
aws_access_key_id=XXXXXXXX
aws_secret_access_key=XXXXXXXX
```

---

### Config File

```text
~/.aws/config
```

Example:

```ini
[default]
region=ap-south-1

[profile dev]
region=ap-south-1

[profile prod]
region=us-east-1
```

### Screenshot

```text
screenshots/04-profile-storage.png
```

---

## Using a Specific Profile

Normally AWS CLI uses:

```text
default profile
```

Example:

```bash
aws s3 ls
```

---

To use a specific profile:

```bash
aws s3 ls --profile dev
```

Another example:

```bash
aws ec2 describe-instances --profile prod
```

AWS CLI will use the credentials associated with the specified profile.

---

## Verifying Profile Identity

Verify which account a profile belongs to.

Command:

```bash
aws sts get-caller-identity --profile dev
```

Example Output:

```json
{
  "Account": "************",
  "Arn": "arn:aws:iam::************:user/dev-user"
}
```

---

For Production:

```bash
aws sts get-caller-identity --profile prod
```

### Screenshot

```text
screenshots/05-profile-verification.png
```

---

## Practical Scenario

A DevOps Engineer manages:

```text
Development Account
Testing Account
Production Account
```

Instead of reconfiguring credentials repeatedly:

```bash
aws ec2 describe-instances --profile dev

aws ec2 describe-instances --profile test

aws ec2 describe-instances --profile prod
```

This enables safe environment switching.

---

## Commands Practiced
```bash
aws configure list-profiles

aws configure --profile dev

aws configure --profile prod

aws configure list-profiles

aws configure list --profile dev

aws configure list --profile prod

aws sts get-caller-identity --profile dev

aws sts get-caller-identity --profile prod

aws s3 ls --profile dev

aws ec2 describe-regions --profile prod
```
---

## Observations

* Multiple AWS accounts can be managed from one machine.
* Profiles prevent credential overwrites.
* Commands use the default profile unless specified.
* STS verification helps avoid accidental operations in the wrong account.
* Profiles simplify cloud administration significantly.

---

## What I Learned

* What AWS CLI profiles are.
* How profiles store independent configurations.
* How to create and manage profiles.
* How to switch between AWS environments.
* How to verify active profile identities.

---

## Real-World Relevance

AWS Profiles are heavily used by:

* Cloud Engineers
* DevOps Engineers
* Consultants
* Platform Teams
* SRE Teams

Common environments:

```text
dev
test
staging
production
```

Profiles make multi-account management safer and more efficient.

---

## Key Takeaways

* Profiles allow multiple AWS configurations on one machine.
* Each profile maintains its own credentials and settings.
* The `--profile` option selects which configuration to use.
* STS verification helps confirm the active account.
* Profiles are essential for multi-account AWS administration.
