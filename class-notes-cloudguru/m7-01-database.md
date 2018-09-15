# Databases 101 #
- Available Relational DataBase Services on AWS
    - MS SQL
    - Oracle
    - MySQL
    - PostgreSQL
    - Amazon Arora
    - MariaDB
- Non Relational Databases
    - DynamoDB      (key-value)
- Data Warehousing (OLAP)
    - RedShift
- In memory caching
    - ElastiCache
- Graph DB
    - Neptune

* Non relational db terminologies
    * Collection        = Tables
    * Document          = Row
    * Key Value Pair    = Fields

- OLTP vs OLAP (Online Transaction Processing vs Online Analytics Processing)
    - If you need to run a complex analytics query on your system you shouldn't run it on the running production database. Because that would slow down the usual operation of your system. Instead you should create a copy of your current database and run your analytics query on that. There comes the concept of DataWarehousing.

- ElastiCache:
    - Web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud.
    - ElastiCache supports two open-source in-memory caching engines:
        - Memcache
        - Redis


# RDS Lab #
- Create a RDS instance with MySql engine
    * Create a new security group
- Create a new EC2 instance with bootstrap script which installs: php, apache, php-mysql.

*RDS instances are always assigned an Endpoint (DNS) location, but it never gets an IP address.*

* (IMPORTANT) Once our EC2 instance and our RDS instance is up an running, try to ssh to EC2 instance and prepare a php page that tries to connect our MySql database in RDS instance.
    * It will fail. Because the EC2 instance and RDS instance lies behind two different security groups, and they can't communicate to each other by default.
    * We need to go to the security group of our RDS instance and add an Inbound Rule to allow requests coming from EC2's security group.


# RDS - Backups, Multi-AZ & Read Replicas #
- There are two types of Backups for AWS:
    - Automated Backups
    - Database Snapshots

    - Automatic Backups:
        - It allows you to recover your database to any point in time within a "retention period", which is between 1 and 35 days.
        - It takes a daily snapshot and also store transaction logs throughout the day.
        - When you do a recovery, AWS will first choose the most recent daily backup and then apply the transaction logs relevant to that day.
        - Enabled by default.
        - Backups are stored in S3 and you get free storage space equal to the size of your DB. If you have an RDS instance of 10GB, you'll get a 10GB S3 storage for free.
        - During the backup window, storage IO may be suspended.
        - You can define your own backup window.
        - Automatic backups are deleted if you delete the original RDS instance.
    - Database Snapshots:
        - Done manually.
        - They live in your S3 even if you remove the original RDS instance.

- Restoring Backups:
    - If you restore either an Automatic backup or a Snapshot, the restored version will be a new RDS instance with a new DNS endpoint.

- Encryption:
    - Encryption at rest is supported for MySql, Oracle, MS Sql, PostgreSql, MariaDB and Aurora.
    - Encryption is done using AWS Key Management Service (KMS).
    - Once the RDS instance is encrypted, all the data stored at rest is also encrypted, as well its automated backups, read replicas and snapshots.
    - Encrypting an existing database instance is not supported.
    - To use Amazon RDS encryption for an existing database:
        - first create a snapshot
        - make a copy
        - encrypt the copy. Then you can instantiate a new RDS instance with the encrypted snapshot.

**Multi-AZ RDS:**
- It allows you to have an exact copy of your production database in another Availability Zone as a backup. AWS handles the replication. As soon as your application writes to your production database, its also synchronized to the stand by database.
- From the application point of view, you connect the RDS using the DNS name, and in case of production database failure/maintenance work AWS automatically redirects all the requests to the standby database automatically.
*Multi-AZ RDS is only for disaster recovery. it doesn't improve performance*
*In order to achieve improved performance you need read-replicas*

- Multi-AZ database is available for:
    - SQL Server
    - Oracle
    - MySQL
    - PostgreSQL
    - MariaDB
*Arora has by default Multi-AZ support.*

**Read Replicas:**
- Instead of reading data from production database, spread the traffic to other replica databases.
- Those replica databases are synced with the original prod database.
- By default you can have 5 read replicas per production database.
- You can have a read replica of another replica.
- You can have read replica in another AZ or even in a different region.
* Multi-AZ is synchronous and Read Replicas are asynchronous
- Read Replicas are available for:
    - MySQL
    - PostgreSQL
    - MariaDB
    - Aurora
* Read Replica is for scaling. Not for disaster recovery.
- You must have automatic backup turned on in order to deploy read replica.
- You can have read replicas that have Multi-AZ enabled.
- You can promote a Read Replica to be their own database. This will break the replication.
- You can have Read Replica in a second region.
- You can enable encryption to a replica even if the original database is not encrypted.


# DynamoDB #
Amazon DynamoDB is a fast and flexible NoSQL database service. It provides consistent, single-digit millisecond latency at any scale.
- Stored on SSD storage.
- Push button scaling. You can change the size of the database on the fly and there won't be any downtime.
- Spread Across 3 geographically distinct data centers.
- Supports Key-Value and Document (JSON, HTML, XML) storage.
- Authentication and Access control to DynamoDB is managed via AWS IAM.
    - You can allow an user to be able to see only a part of your DynamoDB (i.e. His information only; using a Condition to an IAM policy).

**Consistent Model for Read**
- Eventual Consistent Reads (default): Consistency across all copies of data.
- Strongly Consistent Reads:

**Two types of Primary Key**
- Partition Key: An unique attribute. This key goes to a hash function, and the output of the hash determines the physical location of the data to be stored.
- Composite Key (Partition key + Sort key): 2 items may have the same Partition key, but their Sort key must be different. Offers better performance.

*Using ElastiCache in front of DynamoDB offers high amounts of reads for non-frequently changed data*

- Pricing
    - Write throughput $0.0065 per hour for every 10 units
    - Read  throughput $0.0065 per hour for every 50 units

    - Storage cost of $0.25GB per month


# RedShift: Data Warehousing Service #
RedShift is used for running queries to analyze all your data across your data warehouse and data lake (for management reports).

Configuration types:
- Single Node (160 GB)
- Multi Node
    - Leader Node: Manages client connections and receives queries.
    - Compute Node: Store data and perform queries and computations. (max 128 compute nodes)

**Features:**

*Columnar Data Storage*
- RedShift organizes data by column, which is ideal for analytics (since only columns are involved in the queries.)
- Columnar data are stored sequentially on the storage media, thus requires fewer I/Os.

*Compression*
- Columnar data can be compressed much more than row-based data, because similar data are stored sequentially in a disk.

*MPP: Massively Parallel Processing*
- RedShift automatically distributes data and query load across all nodes.

**Security**

**Availability**
- Only available in 1 AZ


# ElastiCache #
In-memory data stores.

**Types**
- MemCache
- Redis

Your database is under a lot of stress/load. Which solution you should pick?
Tips:
- ElastiCache: If you database is particularly read heavy and not prone to frequent changes.
- RedShift: If your database is under stress because management keep running big OLAP transactions.


# Aurora (RDS) #
MySQL and PostgreSQL compatible relational database built for the cloud.
Aurora DB cluster consists of one or more DB instances and a cluster-volume that manages the data for those DB instances.

**Key Features:**
- An Aurora cluster-volume can grow to a maximum size of 64 terabytes.
- Aurora Clusters replica lag is less than 100 milliseconds after the primary instance has written an update.

Two types of DB instances make up an Aurora DB cluster:
- Primary DB instance:
    - Supports read and write operations.
    - Each Aurora DB cluster has one primary DB instance.
- Aurora Replica:
    - Connects to the same storage volume as the primary DB instance.
    - Supports only read operations.
    - Each Aurora DB cluster can have up to 15 Aurora Replicas.

**Features**
- Auto scaling.
- An Aurora cluster-volume can grow to a maximum size of 64 terabytes
- 2 copies of data in each AZ, with minimum of 3 AZ. (6 copies of your data storage is maintained ((not computation-instance))).
- Designed to transparently handle the loss of up to 2 copies of data without affecting database write availability, and up to 3 copies without affecting read availability.
- Storage is self healing.

2 types of replicas:
- Aurora replicas (15 replicas)
- MySQL Read Replicas (5 replicas)

By default Aurora maintains 6 copies of your data, but only one Aurora Instance is created. So you might want to create failover instances. Just select your Aurora Instance's actions and select Create Replica. While creating replica select Failover priority "Tier-1" to make it the first failover. Failover position is determined by the Tier Number.


