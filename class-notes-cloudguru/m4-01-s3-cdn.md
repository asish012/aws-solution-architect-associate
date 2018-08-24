### S3 101: Simple Storage Service ###
- Its an Object-based storage.
- Files can be from 0 Bytes to 5 TB.
- Unlimited storage.
- Files are stored in Buckets.
- S3 uses a universal namespace. Each S3 bucket name must be unique globally.
- S3 bucket link example: https://s3-eu-west-1.amazonaws.com/my_bucket_name
- On a successful upload of a file to s3, you'll receive a HTTP 200 code.
* S3 does not require region selection. Its global. But S3 buckets are region specific.

### S3: Data Consistency Model ###
- Read after Write consistency for PUTS of new objects.
- Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate update and delete operation)-

### S3: In Depth ###
- S3 is a simple key-value storage.
    - Key: The name of the object
    - Value: The data (sequence of bytes)
    - Version ID
    - Metadata (e.g. tag)
    - Sub-resources
        - Access Control List (ACL)
        - Torrent
- Availability: 99.99%
- Durability: 99.99999999999% (11 x 9)
- Tiered Storage Available: Different types of S3 buckets.
- Lifecycle Management (e.g. over 30 days old files will be moved to archive)
- Versioning
- Encryption
- Secure your data using Access Control Lists and Bucket Policies.
    - Bucket Policy: Policy applied on Bucket level
    - Access Control List: Applied on individual files

### S3: Storage Tiers/Classes ###
- S3 Standard:
    - Availability: 99.99%
    - Durability: 99.99999999999%
    - Redundantly stored across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.
        * Devices: disks
        * Facilities: Availability zone
- S3 IA (Infrequently Accessed):
    - Retrieval fee charged
- S3 1 Zone IA:
    - Infrequently accessed data stored in only one availability zone.
- Glacier (Data Archiver)
    - Expedited: Data archived within few minutes
    - Standard: Data archived takes 3-5 hours
    - Bulk: Data archived takes 5-12 hours

|                             | S3 Standard     | S3 Standard-IA  | S3 One Zone-IA  | Glacier         |
|-----------------------------|-----------------|-----------------|-----------------|-----------------|
| Durability                  | 99.99999999999% | 99.99999999999% | 99.99999999999% | 99.99999999999% |
| Availability                | 99.99%          | 99.9%           | 99.5%           | NA              |
| Availability SLA            | 99.9%           | 99%             | 99%             | NA              |
| Availability Zones          | >=3             | >=3             | 1               | >=3             |
| Min capacity charge per obj | NA              | 128KB *         | 128KB *         | NA              |
| Min storage duration charge | NA              | 30 Days         | 30 Days         | 90 Days         |
| Retrieval Fee               | NA              | per GB          | per GB          | per GB **       |
| First byte latency          | milliseconds    | milliseconds    | milliseconds    | minutes / hours |
| Storage type                | Object          | Object          | Object          | Object          |
| Lifecycle transitions       | Yes             | Yes             | Yes             | Yes             |

* SLA: Service Level Agreements

### S3: Charges ###
- Charged for:
    - Storage: per GB
    - Number of request
    - Storage management pricing: For metadata (tags etc)
    - Data transfer pricing: When we do cross region replication (transfer data from one region to another)
    - Transfer acceleration: It uses CloudFront's backbone in order to enable fast and secure data transfer to CloudFront's distributed Edge locations. And from there it serves the end user.


### S3 101 summary ###
- S3 is object-based storage.
- Files can be from 0 Bytes to 5 TB.
- Unlimited storage.
- Files are stored in Buckets.
- S3 is a universal namespace. Bucket names must be unique globally.
- example:
    - <https://><s3>-<region>.amazonaws.com/<bucket_name>
    - https://s3-eu-west-1.amazonaaws.com/my_bucket_name

* Read after Write consistency for PUTS of new objects.
* Eventual consistency for overwrite PUTS and DELETES
* Storage classes/tiers: S3 Standard | S3 IA | S3 One Zone IA | Glacier
* S3 Objects:
    - Key
    - Value
    - Version ID
    - Metadata
    - Sub-resources
        - Access Control List (ACL)
        - Torrent
* S3 is not for OS or DB
* HTTP 200 on successful upload


### CloudFront - Content Delivery Network (CDN) ###
- System of distributed servers located in different geographic locations to ensure faster access via caching.

- Edge Location: Location where the content will be cached. its not "aws region" or "availability zone".
- Origin: Origin is the origin of all files that CDN will distribute to the Edge Location closest to the user.
- Distribution: the CDN which consists of a collection of Edge Location.
    - 2 types of distributions:
        * Web Distribution: Used for Websites.
        * RTMP Distribution: Used for Media streaming.

* CDN works with other amazon web services as well as works seamlessly with any non-AWS origin server which stores the original definitive versions of your files.

- Edge location is not only for read-access, users can write to it too.
- Objects are cached for life of the TTL (time to live).
- You can clear cached objects, but will be charged.


### S3 Security & Encryption ###
- By default all newly created buckets are PRIVATE.
- There are 2 ways to control access to your bucket:
    - Bucket Policy: applies to the entire bucket and all objects/files inside the bucket.
    - Access Control Lists (ACL): allows you to control per object basis access.

* S3 buckets can be configured to create access logs, which logs all requests made to the S3 bucket.


### S3 Encryption ###
* 4 different methods of encryptions on S3.

- 2 ways of encryptions
- In Transit: When you send data from your machine to S3 bucket.
    - SSL/TLS:
- At Rest
    - Server side (3 methods):
        * S3 Managed Key (SSE-S3): Each object managed with a unique key applying strong multi-factor encryption.
            > To provide additional safeguard, amazon encrypts the key with a master-key and regularly rotate the master-key.
            > Amazon handles all the keys for you. Its a AES 256 bit.
        * AWS Key Management Service (KMS) managed keys - (SSE-KMS):
            > Provides order trial: information about who is accessing your objects, who is decrypting and what and when?
            > Offers Envelop key
        * Server side encryption with customer provided keys - (SSE-C):
    - Client side (method #4):
        > You encrypt the data and just upload it to S3
