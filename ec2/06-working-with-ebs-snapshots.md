# Working with EBS Snapshots

## Objective

Create a snapshot of an EBS volume, restore a new volume from the snapshot, and verify that data is preserved.

---

## Services Used

* Amazon EBS
* Amazon EC2

---

## Concepts Learned

* Snapshots are point-in-time backups of EBS volumes.
* Snapshots are stored in Amazon S3 (managed by AWS).
* New EBS volumes can be created from existing snapshots.
* Snapshots are incremental, reducing storage consumption and backup time.

---

## What I Did

* Stored test data on an EBS volume.
* Created a snapshot of the volume.
* Created a new EBS volume from the snapshot.
* Attached the restored volume to an EC2 instance.
* Mounted the volume and verified data recovery.

---

## Commands Practiced

### Identify Mounted Volumes

```bash id="ax4n7e"
lsblk
```

### Create Test Data

```bash id="8myr2u"
echo "Snapshot Test Data" > /data/test.txt
```

### Verify Data

```bash id="n2up4h"
cat /data/test.txt
```

### Create Snapshot

```bash id="6b7qfk"
aws ec2 create-snapshot \
--volume-id vol-xxxxxxxx \
--description "EBS Snapshot Lab"
```

### View Snapshots

```bash id="vczc3o"
aws ec2 describe-snapshots \
--owner-ids self
```

### Create Volume from Snapshot

```bash id="quaz3z"
aws ec2 create-volume \
--snapshot-id snap-xxxxxxxx \
--availability-zone ap-south-1a
```

### Attach Restored Volume

```bash id="mxx5z8"
aws ec2 attach-volume \
--volume-id vol-xxxxxxxx \
--instance-id i-xxxxxxxx \
--device /dev/sdf
```

### Verify Restored Data

```bash id="5btt2y"
sudo mount /dev/xvdf /restore

cat /restore/test.txt
```

---

## Validation

Verified:

* Snapshot creation completed successfully.
* New volume created from snapshot.
* Volume attached successfully.
* Original data available after restoration.

---

## Problem Encountered

### Problem

Restored volume appeared empty.

### Investigation

Checked:

```bash id="9mbjzu"
lsblk

sudo blkid
```

Verified correct volume and filesystem.

### Resolution

Mounted the correct partition and rechecked the data.

---

## Observations

* Snapshot creation does not impact application availability.
* Restored volumes contain all data present at snapshot time.
* Snapshots can be used to recover deleted or corrupted volumes.
* Multiple volumes can be created from a single snapshot.
* Snapshot storage is generally cheaper than keeping unused volumes.

---

## What I Learned

* How AWS backups EBS data using snapshots.
* The relationship between snapshots and restored volumes.
* Basic disaster recovery workflow.
* Snapshot-based cloning of storage.
* Importance of validating backups through restoration testing.

---

## Recovery Scenario

### Situation

Application data volume becomes corrupted.

### Recovery Approach

1. Locate latest healthy snapshot.
2. Create a new EBS volume.
3. Attach to EC2 instance.
4. Mount volume.
5. Validate application data.

This approach minimizes downtime and data loss.

---

## Screenshots

Add screenshots for:

* Snapshot Creation
* Snapshot Completed State
* Volume Created from Snapshot
* Volume Attachment
* Data Recovery Verification

---

## Architecture Notes

```text id="5v7rtx"
Original EBS Volume
          │
          ▼
      Snapshot
          │
          ▼
 New EBS Volume
          │
          ▼
 EC2 Instance
          │
          ▼
 Restored Data
```

---

## Key Takeaway

Snapshots provide a simple and reliable mechanism for backup, recovery, migration, and cloning of EBS volumes. Creating backups is important, but validating recovery from those backups is equally important.

---

## What Makes This Valuable

This lab demonstrates:

* Backup operations
* Disaster recovery concepts
* Storage restoration
* AWS CLI usage
* Linux storage validation

These are common responsibilities in Cloud Engineer, DevOps, and Infrastructure roles.

---

## Next Steps

* Create custom AMIs
* Compare snapshots and AMIs
* Expand EBS volume size
* Explore EBS volume encryption
* Practice volume migration between instances
