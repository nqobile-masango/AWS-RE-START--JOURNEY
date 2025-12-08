<img width="1366" height="768" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/c290734e-07a0-44d2-95ab-26a6f8a1a930" /> # Working with Amazon EBS

## Lab overview
In this lab, I learn to create an EBS volume, attach it to an EC2 instance, set up a file system on it, and make a snapshot backup.

## Objectives
By the end of this lab, you will be able to do the following:
- Create an EBS volume.
- Attach and mount an EBS volume to an EC2 instance.
- Create a snapshot of an EBS volume.
- Create an EBS volume from a snapshot.
## Challange 
<img width="1366" height="290" alt="lab-1 (1)" src="https://github.com/user-attachments/assets/6f62e47d-6398-4797-b202-20b8660a9409" />


## Task 1: Creating a new EBS volume
I open EC2, check the Lab instance’s Availability Zone, then go to Volumes to see the existing 8 GiB EBS volume attached to it.

Choose Create volume, and configure the following options:
- Volume type: Choose General Purpose SSD (gp2).
- Size (GiB): Enter 1. 
- Note: You might be restricted from creating large volumes.
- Availability Zone: Choose the same Availability Zone as your EC2 instance (which is us-west-2a in this case).

Your configurations must look like the following picture:
  
<img width="711" height="543" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/1a962e8c-a966-4e56-b71f-a6ceef66ca5d" />

In the Tags -optional section, choose Add tag, and configure the following options:
- Key: Enter Name.
- Value: Enter My Volume.
- Choose Create volume.

Your configurations must look like the following picture:

<img width="1314" height="447" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/d9504896-c975-4845-9c34-aae2e51776dc" />

## Task 2: Attaching the volume to an EC2 instance
You now attach your new volume to an EC2 instance.

Select My Volume.

From the Actions menu, choose Attach volume.

<img width="1121" height="320" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/3595b6f8-faf3-4df8-a67c-489e7b424126" />

From the Instance dropdown list, choose the Lab instance.

<img width="1346" height="628" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/9a2a8b21-8afa-4746-9f07-cce7ca699450" />


Choose Attach volume.

The Volume state of your new volume is now In-use.

<img width="1103" height="233" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/be191284-7f0c-4c0b-a677-5b8264e140fb" />

## Task 3: Connecting to the Lab EC2 instance
On the AWS Management Console, in the Search bar, enter and choose EC2 to open the EC2 Management Console.

In the navigation pane, choose Instances.

From the list of instances, select the Lab instance.

<img width="1307" height="554" alt="Screenshot (9)" src="https://github.com/user-attachments/assets/667b4d71-41be-4bb8-9f97-51fdd3effdbb" />

Choose Connect.

On the EC2 Instance Connect tab, choose Connect.

## Task 4: Creating and configuring the file system
To view the storage that is available on your instance, in the EC2 Instance Connect terminal, run the following command:
________________________________________________
df -h
___________________________________________________

<img width="1291" height="274" alt="Screenshot (10)" src="https://github.com/user-attachments/assets/8252ba0a-9c93-4191-9831-cb069bfe6884" />

You should see output similar to the following:
<img width="1337" height="401" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/1ac5c967-50d4-4cd4-a349-9eb6c6885b68" />

To create an ext3 file system on the new volume, run the following command:
_________________________________________________________
sudo mkfs -t ext3 /dev/sdb
_____________________________________________________________
The results from the ouput:
<img width="1339" height="393" alt="Screenshot (12)" src="https://github.com/user-attachments/assets/66de8d3b-1129-4cdb-9463-b9b62b5303eb" />

To create a directory to mount the new storage volume, run the following command:
______________________________________________________
sudo mkdir /mnt/data-store
______________________________________________________
<img width="1331" height="287" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/36e310d1-b9fb-4cc2-8aeb-39a5cb4bc8fe" />

To mount the new volume, run the following command:
______________________________________________________
sudo mount /dev/sdb /mnt/data-store
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
__________________________________________________________
To view the configuration file to see the setting on the last line, run the following command:
_________________________________________________________________
cat /etc/fstab
_______________________________________________________________
To view the available storage again, run the following command:
_______________________________________________________________
df -h
_________________________________________________________________

The results should be the following:
<img width="1335" height="156" alt="Screenshot (13)" src="https://github.com/user-attachments/assets/6c2139ed-61e9-4f11-98f2-d96813349eb7" />

To create a file and add some text on the mounted volume, run the following command:
____________________________________________________________________
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
__________________________________________________________________
To verify that the text has been written to your volume, run the following command:
______________________________________________________________________
cat /mnt/data-store/file.txt
_________________________________________________________________________

## Task 5: Creating an Amazon EBS snapshot
On the EC2 Management Console, choose Volumes, and select My Volume.

From the Actions menu, choose Create snapshot.

In the Tags section, choose Add tag, and then configure the following options:
- Key: Enter Name.
- Value: Enter My Snapshot.-

<img width="1348" height="551" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/9c50a3e8-dcf1-4caa-af52-f2ac19d09b8f" />

Choose Create snapshot.
<img width="1095" height="293" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/e764da1d-c369-46b9-aff6-28af659fcbe5" />

In your EC2 Instance Connect terminal window, to delete the file that you created on your volume, run the following command:
________________________________________________________________________
sudo rm /mnt/data-store/file.txt
_________________________________________________________________________

To verify that the file has been deleted, run the following command:
__________________________________________________________________
ls /mnt/data-store/file.txt
_______________________________________________________________
<img width="1336" height="494" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/1fc2dec8-f387-4d8e-99d0-1a620dbd245f" />
 Don`t let that little text stressed you. It`s supposed to be that way.
# Task 6: Restoring the Amazon EBS snapshot

           Task 6.1: Creating a volume by using the snapshot

On the EC2 Management Console, select My Snapshot.

From the Actions menu, choose Create volume from snapshot.

For Availability Zone, choose the same Availability Zone that you used earlier.

In the Tags - optional section, choose Add tag, and then configure the following options:
- Key: Enter Name.
- Value: Enter Restored Volume.
  
  <img width="1348" height="551" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/3a963185-7d53-4d54-af58-64401a95e1a5" />
Choose Create volume.

- To see your new volume, in the left navigation, choose Volumes.
- The Volume status of your new volume is Available.
  <img width="1095" height="293" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/0bbfa842-b322-4ddf-831a-140e9fe75000" />

            Task 6.2: Attaching the restored volume to the EC2 instance

Select Restored Volume.

From the Actions menu, choose Attach volume.

From the Instance dropdown list, choose the Lab instance.

For the Device name field, choose /dev/sdc. You use this device identifier in a later task.
<img width="1318" height="509" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/c1485cff-c7ac-4c45-9fc4-7cfbc921ed4a" />

Choose Attach volume.

The Volume status of your volume is now In-use
<img width="1094" height="252" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/e604b614-aea6-482f-bd14-06c23e1b5677" />

            Task 6.3: Mounting the restored volume
To create a directory for mounting the new storage volume, in the EC2 Instance Connect terminal, run the following command:
__________________________________________________
sudo mkdir /mnt/data-store2
___________________________________________________
To mount the new volume, run the following command:
____________________________________________________
sudo mount /dev/sdc /mnt/data-store2
_____________________________________________________
To verify that the volume that you mounted has the file that you created earlier, run the following command:
______________________________________________________
ls /mnt/data-store2/file.txt
_______________________________________________________
