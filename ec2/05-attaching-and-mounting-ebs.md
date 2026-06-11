# Attaching and Mounting an EBS Volume

## Objective

Create an EBS volume, attach it to an EC2 instance, format it with a filesystem, mount it, and verify persistent storage.

---

## Services Used

* Amazon EC2
* Amazon EBS

---

## Concepts Learned

* EBS provides block-level storage for EC2 instances.
* A newly attached EBS volume is a raw disk and must be formatted before use.
* Data stored on EBS persists independently of the EC2 instance lifecycle.
* A volume must be mounted before applications can store data on it.

---

## What I Did

* Created a new EBS volume.
* Attached the volume to an EC2 instance.
* Verified the new block device from Linux.
* Created an ext4 filesystem.
* Mounted the volume.
* Stored test data.
* Configured automatic mounting after reboot.

---

## Commands Practiced

### View Available Disks

```bash id="1f6v7w"
lsblk
```

### Create Filesystem

```bash id="wh4o8g"
sudo mkfs.ext4 /dev/xvdf
```

### Create Mount Directory

```bash id="wr61i6"
sudo mkdir /data
```

### Mount Volume

```bash id="a9x3gw"
sudo mount /dev/xvdf /data
```

### Verify Mount

```bash id="pw7vha"
df -h
```

### Create Test File

```bash id="d4j84z"
echo "EBS Volume Test" > /data/test.txt
```

### Verify Data

```bash id="5yzn5h"
cat /data/test.txt
```

### Get UUID

```bash id="o7h6nl"
sudo blkid
```

### Configure Persistent Mount

```bash id="0f74my"
sudo nano /etc/fstab
```

Example entry:

```text id="jrllyr"
UUID=<volume-uuid> /data ext4 defaults,nofail 0 2
```

---

## Validation

Verified:

* Volume appeared as a new block device.
* Filesystem created successfully.
* Volume mounted correctly.
* Test file persisted on storage.
* Mount survived instance reboot.

---

## Problem Encountered

### Problem

Volume attached but not visible inside Linux.

### Investigation

```bash id="8bqvaf"
lsblk
```

Checked attached devices and verified attachment status in AWS.

### Resolution

Refreshed device list and confirmed correct device name.

---

## Observations

* Attaching a volume does not automatically make it usable.
* Formatting is required before storing data.
* Mounting provides an access path within the filesystem.
* EBS behaves similarly to adding a new hard disk to a physical server.
* Data remains available even after stopping the EC2 instance.

---

## What I Learned

* Difference between attaching and mounting storage.
* How Linux identifies block devices.
* Filesystem creation using ext4.
* Persistent storage configuration using `/etc/fstab`.
* Basic EBS administration workflow.

---

## Screenshots

Add screenshots for:

* EBS Volume Creation
* Volume Attachment
* `lsblk` Output
* Mounted Volume
* Test File Verification

---

## Architecture Notes

```text id="x0ag3l"
EC2 Instance
      │
      ▼
Attached EBS Volume
      │
      ▼
Filesystem (ext4)
      │
      ▼
Mount Point (/data)
      │
      ▼
Application Data
```

---

## Key Takeaway

This lab demonstrated how additional storage is provisioned and integrated into a Linux server. The process closely resembles real-world server administration where new disks are attached, formatted, mounted, and prepared for application data.

---

## Next Steps

* Create EBS snapshots
* Restore volumes from snapshots
* Expand EBS volume size
* Explore EBS volume types
* Create custom AMIs using EBS-backed instances
