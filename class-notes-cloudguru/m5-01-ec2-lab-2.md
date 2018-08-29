> 34 - 35

### EC2 Security Group (IMPORTANT) ###
- Start apache web server on every boot-up.
    `chkconfig httpd on`

- All inbound traffic is Block by default.
- All outbound traffic is allowed by default.
- There is no way to add a deny rules in security group, by default everything is denied and you have to allow particular rules.
- Any change made in Security Group is applied immediately.
- Any rule you add as "Inbound Rule" will be served, even if there no "Outbound Rule" defined. Because Security Group is "Stateful", thats why adding an Inbound rule adds corresponding Outbound rule.
- You can add multiple security group to a single EC2 instance from menu: Actions -> Networking -> Change Security Group.
- You can have multiple EC2 instances within a security group.

**Difference between Security Group and Network Access Control List**
- Security group is Stateful, Network Access Control List is Stateless.
- You can't block/deny requests coming from particular IP address using Security Group, you can do it using Network Access Control List.


### EBS Volumes (IMPORTANT) ###
- All added volumes has to be in the same Availability Zone of the EC2 instance where you want to mount them.
- We can change volume type and size of SSD volumes even when the EC2 instance is running. However you can't do that on Magnetic Standard volumes.
- If you want to move one EBS Volume from one Availability zone to another:
    - You have to take a snapshot of the volume and then create another volume. you can change Volume type, size, and availability zone.
    - You can also copy the snapshot and move it to another AZ.
    - You can create an Image as well and boot it as another EC2 as well.
- If you terminate your EC2 instance it will only terminate the root EBS. Other mounted EBS has to be terminated manually.
- Snapshots needs to be deleted manually as well.
- Snapshots are stored in S3 but not visible in S3 dashboard.
- You can create Amazon Machine Images (AMI) from snapshots.
- Snapshots of encrypted volumes are encrypted as well.
- Only un-encrypted snapshots can be shared with other users.
