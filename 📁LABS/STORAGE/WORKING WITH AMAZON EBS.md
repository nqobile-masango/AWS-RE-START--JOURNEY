Task 1: Creating a new EBS volume

Open EC2 console and locate the Lab instance.

Note its Availability Zone.

Create a 1-GiB gp2 volume in the same Availability Zone.

Tag it My Volume and confirm it shows as Available.

Task 2: Attaching the volume to an EC2 instance

Select My Volume → Attach volume.

Choose the Lab instance.

Set device name to /dev/sdb.

Volume state changes to In-use.

Task 3: Connecting to the EC2 instance

Open EC2 Instance Connect for the Lab instance.

Connect via browser terminal.

Use this terminal for all remaining commands.

Task 4: Creating and configuring the file system

Run df -h to view existing disks.

Format new volume: sudo mkfs -t ext3 /dev/sdb.

Create and mount directory /mnt/data-store.

Add mount entry to /etc/fstab for persistence.

Verify mount and create file.txt on the volume.

Task 5: Creating an EBS snapshot

Select My Volume → Create snapshot.

Tag it My Snapshot and wait for completion.

Delete file.txt from the mounted volume.

Confirm the file is removed.

Task 6: Restoring the snapshot
6.1 Create volume from snapshot

Select My Snapshot → Create volume.

Use same Availability Zone and tag it Restored Volume.

6.2 Attach restored volume

Attach to instance as /dev/sdc.

6.3 Mount restored volume

Create /mnt/data-store2.

Mount using sudo mount /dev/sdc /mnt/data-store2.

Verify that file.txt has been restored from the snapshot.
