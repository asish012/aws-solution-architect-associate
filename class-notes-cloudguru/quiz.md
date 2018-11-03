**Issues with connecting to an S3 bucket from an EC2 instance residing inside a VPC, using a gateway VPC endpoint**
- Check route table settings to Amazon S3
    - Be sure there's a route to Amazon S3 using the gateway VPC endpoint.
- Security group outbound rules of EC2 instance
    - be sure the available outbound rules allow traffic to Amazon S3
- Network ACL rules of EC2 instance
    - be sure the rules allow inbound return traffic from Amazon S3 on ephemeral TCP ports 1024-65535.
    - be sure the rules allow traffic to Amazon S3.
- S3 bucket policy
    - Be sure the bucket policy allows access from the gateway VPC endpoint
- IAM policy
    - Be sure the users associated with the IAM user or role have the correct permissions to access Amazon S3


**Limiting Limiting Access to S3 Content**
- Using an Origin Access Identity (OAI)
- Restricting Content with Signed URLs and Signed Cookies
- Using AWS WAF (web application firewall) to Control Access to Your Content
- Geo-Restricting Content

**Securing Access to S3 Content**
- Using HTTPS with CloudFront
- Using Alternate Domain Names and HTTPS
- Using Field-Level Encryption to Help Protect Sensitive Data

*> S3 is an "object storage" <*
*> EFS is a "file storage"   <*


**IAM-AMI**
- IAM is not az specific, they are valid across entire account.
- AMI is region specific, to use the AMI in another region, you must copy it to that region.


**Logs**
- VPC Flow Logs:
    - VPC Flow Logs captures IP traffic going to and from network interfaces in your VPC. Flow log data is stored using Amazon CloudWatch Logs.
    - You can create a flow log for a VPC, a subnet, or a network interface.
- CloudTrails
    - To track your changes.
    - Enables governance, compliance, operation auditing, and risk auditing.
    - CloudTrail provides:
        - Event history of your AWS account activity; This helps Security analysis, resource change tracking
        - Logs
    * By default, CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE).
- CloudWatch
    - Monitor performance of aws resources.
    - Store logs including CloudTrail logs.


**Tagging**
- Tags help you manage your instances, images, and other Amazon EC2 resources.
- Tags enable you to categorize your AWS resources in different ways, for example, by purpose, owner, or environment.
- EG: You can add tags to production instances and development instances. These tags can then be used while controlling access via an IAM Policy.


**Encryption** with AWS KMS:
* RDS:
    - You can encrypt your Amazon RDS DB instances and snapshots at rest by enabling the encryption option for your Amazon RDS DB instances. Data that is encrypted at rest includes the underlying storage for a DB instances, its automated backups, Read Replicas, and snapshots.
* EBS:
    - EBS Volumes can be encrypted.
    * There is no direct way to encrypt an existing unencrypted volume, or to remove encryption from an encrypted volume.
    - Snapshot can be encrypted while creating a copy of an unencrypted snapshot of an unencrypted EBS volume. Volumes restored from this encrypted copy are also encrypted.
    - A Snapshot from an encrypted volume is already encrypted.
    - When you have access to both an encrypted and unencrypted volume, you can freely transfer data between them. EC2 carries out the encryption and decryption operations transparently.
* EFS:
    - Amazon EFS Now Supports Encryption of Data at Rest.
* S3:
    - Data protection refers to protecting data while _in-transit_ (as it travels to and from Amazon S3) and _at rest_ (while it is stored on disks in Amazon S3 data centers). You can protect data in transit by using SSL or by using client-side encryption. You have the following options of protecting data at rest in Amazon S3:
        - _Server-Side Encryption_: S3 will encrypt your object before saving it on disks and will decrypt it when you download the objects.
        - _Client-Side Encryption_: You can encrypt data in the client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.


**Elastic Beanstalk**
- With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud.
- You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.
- Elastic Beanstalk supports the deployment of web applications from Docker containers.


**OpsWorks**
- AWS OpsWorks is a configuration management service that helps you configure and operate applications in a cloud enterprise by using Puppet or Chef.


**Amazon Kinesis**
- Amazon Kinesis makes it easy to collect, process, and analyze video and data streams in real time.
    - Kinesis Video Streams
    - Kinesis Data Streams
    - Kinesis Data Firehose
    - Kinesis Data Analytics


**Lambda**
- AWS Lambda automatically monitors your lambda function and logs all requests handled by your function and stores logs generated by your code to CloudWatch log.


**AWS managed Database server's availability**
- Enable Read Replicas for the database.
- Enable Multi-AZ for the database.
**Self managed Database server's availability**
- Introduce another EC2 instance in another AZ with replication configured. Thus availability will be achieved.


**S3 PUT/PUTS/DELETE request rate**
- Amazon S3 automatically scales to high request rates. For example, your application can achieve at least 3500 PUT/POST/DELETE and 5500 GET requests _per second per prefix_ in a bucket. There are no limits to the number of prefixes in a bucket.


**Amazon ECS Launch Types**
An Amazon ECS launch type determines the type of infrastructure on which your tasks and services are hosted.
- Fargate Launch Type (managed by AWS): Run your containerized applications without the need to provision and manage the backend infrastructure.
- EC2 Launch Type (managed by You): You run your containerized applications on a cluster of Amazon EC2 instances that you manage.


**AWS Storage Gateway**
- Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration between your on-premises IT environment and the AWS storage infrastructure.
    - _File Gateway_: A file gateway simplifies file storage in Amazon S3, integrates to existing applications through industry-standard file system protocols.
    - _Volume Gateway_: A volume gateway provides cloud-backed storage volumes that you can mount as Internet Small Computer System Interface (iSCSI) devices from your on-premises application servers.
        - _Cached volumes_: You store your data in Amazon Simple Storage Service (Amazon S3) and retain a copy of frequently accessed data subsets locally.
        - _Stored volumes_: You store all your data locally and asynchronously back up point-in-time snapshots of this data to Amazon S3. This provides low-latency access to your entire dataset.
    - _Tape Gateway_: With a tape gateway, you can cost-effectively and durably archive backup data in Amazon Glacier.


**EBS Volume Types**
- General purpose *SSD* (GP2)
    - IOPS:         _up to 10,000_
    - Volume size:  _1GB - 16TB_
    - Throughput:   _160 MiB/s_ (Volumes 170 GiB to 214 GiB: 160; Other volumes 128)
    - Recommended for most workloads
    - System boot volumes
- Provisioned IOPS *SSD* (IO1)
    - IOPS:         _up to 32,000_
    - Volume size:  _4GB - 16TB_
    - Throughput:   _500 MiB/s_
    - Recommended for large database workloads
- Throughput Optimized HDD (ST1)
    - IOPS:         _up to 500_
    - Volume size:  _500GB - 16TB_
    - Throughput:   _500 MiB/s_
    - Big data | Data warehouse | Log processing
    - Can't be boot volume. _It can only be used as additional drives_.
- Cold HDD (SC1)
    - IOPS:         _up to 250_
    - Volume size:  _500GB - 16TB_
    - Throughput:   _250 MiB/s_
    - Lowest cost storage, appropriate for infrequent accessed workloads.
    - Can't be boot volume. _It can only be used as additional drives_.
- Magnetic (Standard)
    - Lowest cost per giga of all EBS volume types that bootable.

**By default, EBS Volumes are replicated within their Availability Zones to protect you from component failure.**

**Snapshots of EBS**
A snapshot is constrained to the region where it was created. After you create a snapshot of an EBS volume, you can use it to create new volumes in the same region. You can also copy snapshots across regions, making it possible to use multiple regions for geographical expansion, data center migration, and disaster recovery.


**Well Architected Framework**
- Design Principle:
    - Apply security at all layers. Subnets, ACL, On instances (firewall, antivirus)
    - Enable traceability
    - Automate responses to security events
    - You are responsible to secure your Data, your Application and the OS
- Shared responsibility model (IMPORTANT):
    - Customers responsibility:
        - Platform (OS)
        - Application
        - IAM
        - SG
        - NACL
    - Amazon's responsibility:
        - Security of the cloud (Physical infrastructure)
        - Applications offered by them: MS SQL SERVER, ...

**Security**
- *Security - Data Protection*
    - Who should have access to your data.
- *Security - Privilege Management*
    - Role based access management.
    - Multi factor access management.
    - Groups or users (HR, Admins, ...)
- *Security - Infrastructure Protection*
    - VPC protection (public/private subnets, service group, nacl rules), multi-factor authentication, ...
- *Security - Detective Controls*

**Reliability**
- Design Principle:
    - Test recovery procedures
    - Automatically recover from failure
    - Scale horizontally to increase aggregate system availability
    - Stop guessing capacity
- *Reliability - .*


**STS**


**RDS Multi-AZ VS Read Replicas**
| Multi-AZ Deployments                                      | Read Replicas                                                       |
| --------------------------------------------------------- | ------------------------------------------------------------------- |
| Synchronous replication – highly durable                  | Asynchronous replication – highly scalable                          |
| Only database engine on primary instance is active        | All read replicas are accessible and can be used for read scaling   |
| Automated backups are taken from standby                  | No backups configured by default                                    |
| Always span two Availability Zones within a single Region | Can be within an Availability Zone, Cross-AZ, or Cross-Region       |
| Automatic failover to standby when a problem is detected  | Can be manually promoted to a standalone database instance          |


**Arora**
- If you have an Amazon Aurora Replica in the same or a different Availability Zone, when failing over, Amazon Aurora flips the canonical name record (CNAME) for your DB Instance to point at the healthy replica, which in turn is promoted to become the new primary. Start-to-finish, failover typically completes within 30 seconds.
- If you do not have an Amazon Aurora Replica (i.e. single instance), Aurora will first attempt to create a new DB Instance in the same Availability Zone as the original instance. If unable to do so, Aurora will attempt to create a new DB Instance in a different Availability Zone. From start to finish, failover typically completes in under 15 minutes.


**ElastiCache**
- ElastiCache offers fully managed in-memory data storage (Redis and Memcached).
- ElastiCache is a popular choice for Gaming, Ad-Tech, Financial Services, Healthcare, and IoT apps.
- It improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory data stores


**Athena**
Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless.


**Trusted Advisor**
Trusted Advisor helps you to reduce cost, increase performance, and improve security by optimizing your AWS environment.
It also provides real time guidance to help you provision your resources following AWS best practices.
### AWS Trusted Advisor analyzes your AWS environment and provides best practice recommendations in these five categories: ###
- Cost Optimization, Performance, Fault Tolerance, Security, and Service Limits (CPFSS)


**Inspector**
Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS. Amazon Inspector automatically assesses applications for vulnerabilities or deviations from best practices.


**RedShift**
To enable access to the cluster from SQL client tools via JDBC or ODBC, you use security groups:
- If you are using the _EC2-Classic_ platform for your Amazon Redshift cluster, you must use _Amazon Redshift security groups_.
- If you are using the _EC2-VPC_ platform for your Amazon Redshift cluster, you must use _VPC security groups_.

_Snapshot_:
Automated snapshots are enabled by default when you create a cluster. Amazon Redshift stores these snapshots internally in Amazon S3 by using an encrypted Secure Sockets Layer (SSL) connection.


**Auto Scaling Group**
- It ensures that the Auto Scaling group does not launch or terminate additional EC2 instances before the previous scaling activity takes effect.
- Its default value is 300 seconds.
- It is a configurable setting for your Auto Scaling group.


**Shared Responsibility Model**
- AWS manages the following assets:
    - Facilities
    - Physical security of hardware
    - Network infrastructure
    - Virtualization infrastructure

- The customer are responsible for:
    - Amazon Machine Images (AMIs)
    - Operating systems and their patches
    - Applications
    - Data in transit
    - Data at rest
    - Data stores
    - Credentials
    - Policies and configuration


### 1200 employees would be granted access to use Amazon S3 for their personal documents. Which of the following will you need to consider so you can set up a solution that incorporates single sign-on feature from your corporate AD or LDAP directory and also restricts access for each individual user to a designated user folder in an S3 bucket?
- Setup a Federation proxy or an Identity provider
- Setup an AWS Security Token Service to generate temporary tokens
- Configure an IAM role

In an enterprise identity federation, you can authenticate users in your organization's network, and then provide those users access to AWS without creating new AWS identities for them and requiring them to sign in with a separate user name and password. This is known as the single sign-on (SSO) approach to temporary access. AWS STS supports open standards like Security Assertion Markup Language (SAML) 2.0, with which you can use Microsoft AD FS to leverage your Microsoft Active Directory. You can also use SAML 2.0 to manage your own solution for federating user identities.


**SWF vs SQS**
- _SWF_: Amazon SWF helps to co-ordinate work across distributed application components. It helps developers build, run, and scale background jobs that have parallel or sequential steps. You can think of Amazon SWF as a fully-managed state tracker and task coordinator in the Cloud. Tasks represent invocation of various processing steps in an application which can be performed by executable code, web service calls, human actions and scripts.
- If your app's steps take more than 500 milliseconds to complete, you need to track the state of processing, and you need to recover or retry if a task fails. There you need SWF.
- _SQS_: Amazon SQS helps to set up a highly decoupled application in AWS.


### Amazon S3 Standard - Infrequent Access (Standard - IA) ###
- Used for data that is accessed less frequently
- Rapid access
- Ideally for long-term storage, backup, and storage for disaster recovery
- Low Latency & High Throughput
- Reduced Redundancy Storage (RRS)


### Which of the following AWS services encrypts data at rest by default? ###
- AWS Storage Gateway
- Amazon Glacier


**> http://169.254.169.254/latest/meta-data/ is the URL that you can use to retrieve the Instance Metadata of your EC2 instance, including the public-hostname, public-ipv4, public-keys et cetera. <**



