# S3 Overview #
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
    - Storage class/tier (Standard, Standard-IA, 1 Zone IA, Glacier).
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


# S3 Versioning #
- Once the versioning is enabled you can't disable it later, you can only suspend it.
- If the versioning is enabled, all versions of the file is actually kept (hidden) in the bucket including the deleted version.
- You can enable "MFA Delete" option on buckets, which offers added layer of security.
- MFA Delete effects following operations
    - Change versioning state of the bucket: Enable/Suspend versioning.
    - Permanently delete and object version.


# S3 Cross Region Replication #
- Versioning must be enabled to your source and destination bucket.
- Regions must be different. You can't replicate bucket within the same region. You can do it with copy command from terminal.
- Files in an existing bucket are not replicated automatically. Only subsequent updated files are replicated automatically.
- Existing objects from source bucket needs to be copied to the destination bucket manually:
    > ` aws s3 cp --recursive s3://source-bucket s3://destination-bucket `
- Manually copied files dont carry version history.
- You can't replicate to multiple buckets or use daisy chaining (need to check latest status).
- Deleting files are replicated.
- Deleting individual version or delete markers from history (restore the file) is not replicated.


# S3 Lifecycle Management & Glacier #
- You can move your S3 buckets objects from one tire to another after certain time. e.g. From Standard to Standard-IA after X days and later move to Glacier after X days.
- It can be used with or without versioning enabled.
- It can be applied to current and previous versions.
- You can also permanently delete objects using Lifecycle management rules.


# CloudFront CDN #
- We can create 2 types of distribution.
    - Web: Static and dynamic website (html, css, php, graphics, ...)
    - RTMP: Streaming media files using Adobe Flash Media Server's RTMP protocol.

**Create Web Distribution**
- Origin Domain Name: Your S3 bucket | Elastic Load Balancers | MediaPackage | MediaStore containers
- Origin Path: Folder within S3. You can specify multiple origins in a single distribution. And you can make a Folder of S3 bucket as origin path.
- Origin ID: This value lets you distinguish multiple origins in the same distribution from one another.
- Restrict Bucket Access: Restrict direct/public access of files within S3 bucket and only allow access via CDN.
- Origin Access Identity:
- ...
- Path pattern: You may want to specify certain file extensions coming from certain folders, and you can specify those rules here as regex.
- Viewer Protocol Policy: HTTP and HTTPS | Redirect HTTP to HTTPS | HTTPS only
- Allowed HTTP methods: "GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE". If you select this option then user uploaded stuffs will first land to an edge location then copied to the source bucket.
- ...
- TTL:
    - Min
    - Max
    - Default (24 hrs)
- Restrict Viewer Access: Only signed URLs or signed cookies will have access.
- ...
- Price Class:
- Alternate Domain Names (CNAMEs):
- SSL Certificate:
- ...
- Default Root Object:
- Logging:
- ...
- ...

*Once the distribution is created the files stored in our S3 bucket will be accessible using the Origin ID link* :
- S3 bucket link: https://s3.eu-central-1.amazonaws.com/bucket-101/thirdtest.txt
- Origin ID link: http://bucket-101.s3.amazonaws.com/thirdtest.txt

* If we want to add multiple origins to the CloudFront that we just created, we'd have to select the CloudFront and go to Origins tab and add other origins (e.g. other S3 bucket)
* To remove files from edge location you have to add Invalidations rules to the distribution (costs applicable).
