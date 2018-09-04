> 36 - 38

# RAID Redundant Array of Independent Disk #
- RAID 0:
    - Striped multiple disks together and mount them as single volume.
    - No redundancy, Good performance.
    - If any of those disks fail you loose the entire RAID array.
- RAID 1:
    - Mirrored exact copy of your disk.
    - Reliable
- RAID 5:
    - Amazon doesn't recommend ever putting RAID 5's on EBS.
    - Uses 3 or more disks, and writes parity/checksum to other disks, so if one of the disks fail, you can regenerate the data from those checksums.
- RAID 10:
    - Combination of RAID 1 and RAID 0.
    - Striping + Mirroring
    - Good redundancy + Good performance

* Disks have limited number of IOs. If you need more IO then you can consider having multiple disks and operate parallel IO operation.
* On AWS you can create multiple EBS volumes and put them together to create a single volume in a RAID (redundant array of independent disk) manner.


# RAID LAB #
*Instantiating a EC2 Windows Server with 4 SSD drives*
- Add a RDP (remote desktop protocol) rule to the inbound rules of your security group.
- Using a Windows Server R2.
- Fill the configuration details of your EC2. VPC, Subnet, IAM, ...
- Add 4 SSD volumes.
- Tag.
- Specify your security group which has RDP rule included.
- Launch
- Create new security key pair. save it locally.
- Get the windows password:
    - EC2 instance actions -> Get windows password
    - Provide the saved security key pair certificate.
    - Decrypt password
- Use Microsoft Remote Desktop
    - Connection name: EC2 public IP
    - PC name: EC2 public IP
    - User name: Administrator
    - Password: <Decrypted password>
*Creating a RAID on Windows Server*
- Disk management on Windows server
- You'll see all 4 mounted SSD volumes
- Delete all volumes
- R-Click on one disk and select New Striped Volume
    - Add all 4 disks
    - Assign drive letter
    - Perform quick format
- You will see your newly created Striped RAID array.

*How to take a Snapshot of a RAID array*
- Since there are multiple disks working at a same time, taking a snapshot is not straight forward.
- Solution: Application consistent snapshot
    - Stop all application from writing to disk.
    - Flush all caches to disk
        - Freeze the file system
        - Unmount the RAID array
        - Shutting down the associated EC2 instance
        - Take snapshot.
        - Start the EC2


# Encrypt Root Device Volume & Snapshot #
- Before taking a snapshot its best practice to Stop the EC2 first.
- After taking a snapshot of a non-encrypted volume we can simply encrypt it, copy it to other location, etc.
- After copying, you can then create a Image (AMI) or Volume from of it. (Snapshots -> Actions -> Create Image)
- Then we can create another EC2 instance (at that region) with that Image (AMI) (will be used as root volume).
- To see newly created Images, go to AMI section under Images. and Launch.
*There are prepared AMIs available for purchase in AWS Marketplace*
*e.g. Security Images that you can use as firewall, and put your instances behind that*

* Amazon Machine Images (AMI) are very useful for scaling. You can prepare and EC2 image with your website and all dependencies installed, and create a Snapshot and create an AMI, and later you can start as many EC2 instances as you want from that Image.

* Don't forget to stop/cleanup your Images, Snapshots and Instances.


#  AMI Types and Root device volumes #
* Two types of Root device volumes:
    * EBS
    * Instance Store

- All AMIs are categorized as either backed by Amazon EBS or backed by Instance Store
**EBS vs Instance Store**
- EBS Volume: The root device of an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot.
- Instance Store Volume: The root device of an instance launched from the AMI is an instance store volume created from a Template stored in Amazon S3.
- You can reboot both volumes without loosing any data.
- For EBS Volumes you can configure in a way that Amazon will not remove the root device on termination. For Instance Store Volume it will always be removed.

**Tips**
- Instance Store Volume is also called Ephemeral Storage.
- Instance Store Volumes can not be stopped. If the underlying host fails, you will loose your data.
