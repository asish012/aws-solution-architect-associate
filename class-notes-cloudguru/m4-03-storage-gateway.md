### Storage Gateway (IMPORTANT) ###
**AWS Storage Gateway is a service that connects an on-premises software appliance with cloud-based storage, to provide seamless and secure integration between an organization's on-premises IT environment and AWS's storage infrastructure.**

*AWS Storage Gateway's software appliance is available as virtual machine image that you install on a host in your datacenter. It supports either VMWare ESXi or Microsoft Hyper-V.*

* Four types of Storage Gateways:
    - File gateway (NFS): To store Flat files (word, pdf, pictures, videos, ...)
    - Volumes Gateway (iSCSI): Blob based storage (to run OS, vm, virtual hdd, ... )
        - Stored Volume: entire data stored on-premise.
        - Cached Volume: recently used data will be on on-premise and rest will be backed off into amazon.
    - Tape Gateway (VTL): backup and archiving solution. uses virtual-tapes.

    * Old names (there were only 3):
        * Gateway Stored Volume
        * Gateway Cached Volume
        * Gateway Virtual Tape Library

- File Gateway:
    - Files are stored as Objects in S3 buckets and accessed through a Network File System (NFS) mount point. (nothing is stored on-premise)
    - Ownership, permissions, and timestamps are durably stored in S3 in the user-metadata.
    - Once objects are transferred to S3, versioning, lifecycle management, cross-region-replication and other policies are managed as normal S3 buckets.

- Volume Gateway: (think it as Virtual Hard Disk)
    - Presents your applications with a virtual disk volumes using iSCSI block protocol. Mounted that virtual disk on-premise, and written to that.
    - Data written to these volumes can be asynchronously backed up as point-in-time snapshots of your volumes and stored in the cloud as Amazon Elastic Block Store (EBS) snapshots.
    - Snapshots are incremental backups that capture only changed blocks.
    - All snapshots are also compressed to minimize your storage usages/charges.
    - Two different types of Volume Gateway:
        - Stored Volume: Data stored on-premise and asynchronously backed up to AWS.
        - Cached Volume: Only frequently accessed files are kept on-premise.

- Tape Gateway - Virtual Tape Library (VTL):
    - Durable, cost-effective solution to archive your data in AWS Cloud.


### SnowBalls ###
Snowball is a petabyte-scale data migration/transport solution (physical transportation).
- Snowball: Onboard storage.
- Snowball Edge: Onboard storage and compute capacity. Can run lambdas.
- Snowmobile: Massive data container back of a 18 wheels track. can transfer Exabytes of data.


### S3 Transfer Acceleration ###
Using CloudFront Edge Network it accelerates your uploads to S3. Instead of uploading directly to your S3 bucket, it gives you a direct link to an Edge Location where you'll upload your files. Direct upload link of your bucket via the edge location looks like:
    `<bucket-name>.s3-acceleration.amazonaws.com`


### Create a static website using S3 ###
- Upload your static html files, make them public and enable Static website hosting properties. Thats it.
- If you want a custom domain name and point that to your static website stored in S3 bucket, you have to ensure the domain name and the S3 bucket name to be exactly same.
- Static website url looks like (EXAM):
    `<bucket-name>.s3-website-<region>.amazonaws.com`


### Summary: Chapter 4 ###
- S3 is Object based storage. Only for flat files not for OS/VM.
- File size can be from 0 Bytes to 5TB.
- On successful upload to S3 you get HTTP 200
- S3 is universal namespace, so must be unique globally.
- Example: `https://s3-<region>.amazonaws.com/<bucket-name>`
- Consistency model:
    - Upload: Read after Write
    - Update/Delete: Eventual consistency
- Storage tiers:
    - S3 Standard
    - S3-IA
    - S3 One Zone - IA
    - Glacier
        - Expedited
        - Standard
        - Bulk
- Fundamentals:
    - Key (name)
    - Value (data)
    - Version ID
    - Metadata
    - Access Control List
- Versioning (pay for each version as all versions are stored as well)
- Once versioning is enabled, you cant disable it. only can suspend it.
- Lifecycle rules.
- Can apply MFA for version setup and delete capability.
- Cross Region Replication (requires versioning)
- Lifecycle management
- CloudFront
    - Edge Location (also can write to edge location)
    - Origin (can have multiple origin)
    - Distribution
        - Web
        - RTMP
    - Object cache has TTL (Time To Live) in seconds
    - Clearing cache objects are charged
- Security
    - Default: Private
    - Access Control
        - Bucket Policy
        - Access Control List
    - Logging
- Encryption
    - In Transit
        - SSL/TLS
    - At Rest
        - Server Side Encryption
            - SSE-S3: S3 Managed Keys
            - SSE-KMS: Envelop key that protects encryption key
            - SSE-C: Customer provided key
        - Client Side Encryption
- Storage Gateway:
    - File Gateway: For flat files
    - Volume Gateway:
        - Stored Volume
        - Cached Volume
    - Gateway Virtual Tape Library (VTL)
- Snowball (import to S3 or export from S3)
    - Snowball standard
    - Snowball edge
    - Snowmobile
- Transfer Acceleration
- Static website
    - scales automatically

**Read S3 FAQ**
