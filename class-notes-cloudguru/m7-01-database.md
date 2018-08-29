### Databases 101 ###
* Available Relational DB Services on AWS
    - MS SQL
    - Oracle
    - MySQL
    - PostgreSQL
    - Amazon Arora
    - MariaDB
* Non Relational Databases
    * Collection        = Tables
    * Document          = Row
    * Key Value Pair    = Fields

    - DynamoDB

* DataWarehousing

* OLTP vs OLAP (Online Transaction Processing vs Online Analytics Processing)
    - If you need to run a complex analytics query on your system you shouldn't run it on the running production database. Because that would slow down the usual operation of your system. Instead you should create a copy of your current database and run your analytics query on that. There comes the concept of DataWarehousing.

* ElastiCache:
    - Web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud.
    - ElastiCache supports two open-source in-memory caching engines:
        - Memcache
        - Redis


### RDS Lab ###
- Create a RDS instance with MySql engine
    * Create a new security group
- Create a new EC2 instance with bootstrap script which installs: php, apache, php-mysql.

**RDS instances are always assigned an Endpoint (DNS) location, but it never gets an IP address.**

* (IMPORTANT) Once our EC2 instance and our RDS instance is up an running, try to ssh to EC2 instance and prepare a php page that tries to connect our MySql database in RDS instance.
    * It will fail. Because the EC2 instance and RDS instance lies behind two different security groups, and they can't communicate to each other by default.
    * We need to go to the security group of our RDS instance and add an Inbound Rule to allow requests coming from EC2's security group.


### RDS - Backups, Multi-AZ & Read Replicas ###
* There are two types of Backups for AWS:
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

* Restoring Backups:
    - If you restore either an Automatic backup or a Snapshot, the restored version will be a new RDS instance with a new DNS endpoint.

* Encryption:
    - Encryption at rest is supported for MySql, Oracle, MS Sql, PostgreSql, MariaDB and Aurora.
    - Encryption is done using AWS Key Management Service (KMS).
    - Once the RDS instance is encrypted, all the data stored at rest is also encrypted, as well its automated backups, read replicas and snapshots.
    - Encrypting an existing database instance is not supported.
    - To use Amazon RDS encryption for an existing database:
        - first create a snapshot
        - make a copy
        - encrypt the copy. Then you can instantiate a new RDS instance with the encrypted snapshot.

* Multi-AZ RDS:
    - It allows you to have an exact copy of your production database in another Availability Zone as a backup. AWS handles the replication. As soon as your application writes to your production database, its also synchronized to the stand by database.
    - From the application point of view, you connect the RDS using the DNS name, and in case of production database failure/maintenance work AWS automatically redirects all the requests to the standby database automatically.
    **Multi-AZ RDS is only for disaster recovery. it doesn't improve performance**
    **In order to achieve improved performance you need read-replicas**

    *Multi-AZ database is available for:*
        *SQL Server*
        *Oracle*
        *MySQL*
        *PostgreSQL*
        *MariaDB*
    *Arora has by default Multi-AZ support.*

* Read Replicas:
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


### DynamoDB ###
Amazon DynamoDB is a fast and flexible NoSQL database service. It provides consistent, single-digit millisecond latency at any scale.
- Spread Across 3 geographically distinct data centres.
- Eventual Consistent Reads (default)
- Strongly Consistent Reads
- Pricing
    - Write throughput $0.0065 per hour for every 10 units
    - Read  throughput $0.0065 per hour for every 50 units

    - Storage cost of $0.25GB per month

* Pricing example:
    -
