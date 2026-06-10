# AWS CLI Installation and Configuration

## Overview

AWS Command Line Interface (AWS CLI) is a tool that allows users to interact with AWS services directly from the command line.

Instead of performing actions through the AWS Management Console, AWS CLI enables cloud resources to be managed through commands, making automation and scripting possible.

This lab documents the installation and initial configuration of AWS CLI on my local machine.

---

## Why AWS CLI?

AWS CLI is widely used by Cloud Engineers, DevOps Engineers, and System Administrators because it allows:

* Faster resource management
* Infrastructure automation
* Scripting repetitive tasks
* Integration with CI/CD pipelines
* Direct interaction with AWS APIs

---

## Lab Objective

* Install AWS CLI Version 2
* Verify successful installation
* Configure AWS credentials
* Configure default region and output format
* Verify connectivity with AWS

---

## Prerequisites

Before starting, I had:

* An AWS Account
* An IAM User
* Access Key ID
* Secret Access Key
* Internet Connection

---

## Installation Process

### Step 1: Download AWS CLI

Downloaded AWS CLI Version 2 installer from AWS.

Purpose:

* Install AWS CLI binaries
* Enable command-line access to AWS services

---

### Step 2: Install AWS CLI

Executed the installer and completed the installation process.

The installer automatically:

* Installs AWS CLI
* Adds required binaries
* Updates system path variables

---

### Step 3: Verify Installation

Command:

```powershell
aws --version
```

Example Output:

```text
aws-cli/2.x.x Python/3.x Windows/AMD64
```

Verification:

Successfully confirmed AWS CLI installation.

---

## AWS Configuration

### Configure Credentials

Command:

```powershell
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

---

## Configuration Details

### Access Key ID

Used to identify the IAM user making AWS requests.

### Secret Access Key

Used to authenticate requests.

### Default Region

Configured:

```text
ap-south-1
```

This region becomes the default for future AWS CLI commands.

### Output Format

Configured:

```text
json
```

This determines how AWS CLI displays command results.

---

## Verification

### Verify Active Identity

Command:

```powershell
aws sts get-caller-identity
```

Purpose:

* Verify credentials
* Confirm account access
* Validate AWS CLI configuration

Example Output:

```json
{
  "UserId": "...",
  "Account": "...",
  "Arn": "..."
}
```

---

## Observations

* AWS CLI communicates directly with AWS APIs.
* Installation alone does not provide AWS access.
* Valid IAM credentials are required.
* AWS CLI stores configuration locally.
* Region selection affects future command execution.

---

## What I Learned

* How AWS CLI interacts with AWS services.
* How authentication works using Access Keys.
* How to configure default regions and output formats.
* How to verify AWS account connectivity.
* The importance of securing IAM credentials.

---

## Commands Used

```powershell
aws --version

aws configure

aws sts get-caller-identity
```

---

## Real-World Relevance

AWS CLI is commonly used for:

* Infrastructure automation
* Resource provisioning
* Cloud administration
* CI/CD pipelines
* DevOps workflows
* Troubleshooting cloud environments

---

## Key Takeaways

* Installed AWS CLI Version 2 successfully.
* Configured AWS authentication locally.
* Verified AWS account access using STS.
* Established the foundation for future AWS CLI automation and administration tasks.
