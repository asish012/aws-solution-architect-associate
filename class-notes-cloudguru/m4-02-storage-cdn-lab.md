### S3 Overview ###
- S3 is global. So when you select S3 service from AWS Console notice that the selected region has been changed to "Global".
- On the other hand, a particular Bucket is not global. When you go to create a Bucket you have to specify a region.
- Bucket name however is global, because a bucket can be accessed via a DNS name.

- You can specify following properties of a bucket:
    - Access control.
    - Versioning.
    - Server access logging that provide details about access requests.
    - Host a static website that doesn't require server side technologies.
    - Object level API activity logging using CloudTrail (Additional Cost).
    - Encryption.
    - Metadata
    - Tags (Bucket level Tag).
    - Transfer acceleration.
    - Event notification.

- You can specify following properties of a object inside a bucket:
    - Access control.
    - Private or public access url.
    - Storage class/tier (Standard, IA, 1 Zone IA, etc).
    - Encryption.
    - Metadata
    - Tags (Object level Tag, etc): Bucket tags are not inherited to objects inside the bucket.

- Different server side encryptions:
    - Amazon S3 Managed Keys (SSE-S3)
    - KMS (SSE-KMS)
    - Customer Provided Keys (SSE-C)

- You can control access to your buckets using:
    - Access Control List (ACL): provide access to other AWS accounts.
    - Bucket Policies:

* By default Buckets and all the Objects inside a bucket is private.


### S3 Versioning ###
- Once the versioning is enabled you can't disable it later, you can only suspend it.
- If the versioning is enabled, all versions of the file is actually kept (hidden) in the bucket including the deleted version.
- You can enable "MFA Delete" option on buckets, which offers added layer of security.
- MFA Delete effects following operations
    - Change versioning state of the bucket: Enable/Suspend versioning.
    - Permanently delete and object version.


### S3 Cross Region Replication ###
- Versioning must be enabled to your source and destination bucket.
- Regions must be different. You can't replicate bucket within the same region. You can do it with copy command from terminal.
- Files in an existing bucket are not replicated automatically. Only subsequent updated files are replicated automatically.
- Existing objects from source bucket needs to be copied to the destination bucket manually:
    > ``` aws s3 cp --recursive s3://source-bucket s3://destination-bucket ```
- Manually copied files dont carry version history.
- You can't replicate to multiple buckets or use daisy chaining (need to check latest status).
- Deleting files are replicated.
- Deleting individual version or delete markers from history will not be replicated.

### S3 Lifecycle Management & Glacier ###
