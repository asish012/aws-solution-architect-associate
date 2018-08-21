### AWS global infrastructure ###
- Geographical regions
    - London, Berlin, NY, CA, ... ...
- Availability zone inside each region
    - At-least 2 availability zones per geographical region (aka. data centers)
- Edge location
    - For caching

All the AWS services sits on top of AWS global infrastructure.

### AWS services: Compute ###
- EC2: Elastic Compute Cloud:
- EC2 Container Service:
    Runs docker containers.
- Elastic Beanstalk:
    (more important for developers and sysadmins)
- Lambda:
    Upload your code and control when it executes. Your lambda function will execute based on some events.
- Lightsail:
- Batch: (no exam questions)

### AWS services: Storage ###
- S3:
    Object based storage. Upload data into buckets.
- EFS:
    Elastic File System
- Glacier:
    Data archiver
- Snowball:
    Bring large amount of data in terabytes directly write into disks
- Storage Gateway:
    VMs in data-centers that replicates data into S3

### AWS services: Databases ###
- RDS: Relational database service
- DynamoDB: Non-relational db
- Elasticache: Query from db and cache
- Red Shift: Built for data warehousing

### AWS services: Migration ###
- AWS Migration Hub:
    Tracking service during migration to AWS from private server and integrate with other AWS services.
    Visualize the migration process and progress
- Application Discovery Service:
    Applications and their dependencies
- Database Migration Service:
- Server Migration Service:
- Snowball:
    It works as database service and also as migration service.
    Migrates large amount of data into AWS

### AWS services: Networking and Content Delivery ###
- VPC: (IMPORTANT): Virtual data center. You can configure firewalls, availability zone, network side address ranges, network route table etc...
- CloudFront: Content delivery network.
- Route53: DNS Service.
- API Gateway: (IMPORTANT): Create your own API for your other services.
- Direct Connect: (IMPORTANT): Directly connect your corporate network to AWS and directly connect to your VPC.

### AWS services: Developer Tools ###
<!-- Not very important for architect exam, but very important for developing -->
- CodeStar: Code management/project management/collaboration tool tool, includes contentious integration tools
- CodeCommit: Source control (store your source), store your own private git repository within codecommit.
- CodeBuild: Compile your code
- CodeDeploy: Automate code deployment to your EC2 instances or on premise instances or lambda functions.
- CodePipeline: Continuous delivery service and you can model and visualize and automate the steps to release your software.
- X-Ray: To debug and analyze your application, including requests tracing.
- Cloud9: IDE to write your code.

### AWS services: ###
### AWS services: ###
### AWS services: ###
### AWS services: ###
