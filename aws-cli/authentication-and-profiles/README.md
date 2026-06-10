# Authentication and Profiles

AWS CLI uses authentication to verify the identity of a user before allowing access to AWS resources.

After authentication is configured, profiles can be used to manage multiple AWS accounts and environments from a single machine.

This section documents how AWS CLI credentials are configured, how authentication works, and how profiles simplify multi-account administration.

## Topics Covered

### 1. AWS CLI Authentication

Learn:

* How AWS CLI authenticates requests
* Access Key ID and Secret Access Key
* IAM User credentials
* Credential storage locations
* Authentication verification using AWS STS

File:

```text
01-aws-cli-authentication.md
```

---

### 2. AWS CLI Profiles

Learn:

* Default profile
* Named profiles
* Managing multiple AWS accounts
* Switching between environments
* Profile-specific command execution

File:

```text
02-aws-cli-profiles.md
```

---

## Directory Structure

```text
authentication-and-profiles/
│
├── README.md
├── 01-aws-cli-authentication.md
├── 02-aws-cli-profiles.md
└── screenshots/
```

---

## Learning Outcomes

After completing this section, I will be able to:

* Configure AWS CLI authentication securely
* Understand how AWS validates identities
* Manage multiple AWS configurations
* Switch between AWS environments safely
* Verify active identities before performing operations

---

### Next Step

After understanding authentication and profiles, continue to:

```text
sts/
```

to learn how AWS Security Token Service (STS) is used to verify identities and manage temporary credentials.