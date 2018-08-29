> 49 - 51

### Elastic File System (EFS) Basics ###
- Its a file storage service for Amazon Elastic Compute Cloud (EC2) instances.
- Storage capacity is not bounded. growing and shrinking happens automatically as you add and remove files.
- Supports the Network File System version 4 (NFSv4)
- It can scale up to the petabytes.
- Can support thousands of concurrent NFS connections.
- Data is stored across multiple AZs within a region.
* EFS is block based storage and not object based.
* We can share stored data with other EC2 instances.

**EFS Lab**
We can create a single File System and mount it to multiple EC2 instances. Single resource multiple instances.
- Create an EFS. When created should be available in all the AZs in the Region.
- Create 2 EC2 instances (in separate AZ, within same security group as the EFS volume)
- Create a Load Balancer
- Once the instances are launched, mount the EFS to /var/www/html location. So that if we write our index.html in one instance it will be shared to other instances who mounted the EFS.
    - `sudo mount -t nfs4 $(curl -s http://169.254.169.254/latest/meta-data/placement/availablity-zone).fs-XXXXXXXX.efs.us-west-2.amazonaws.com:/ /var/www/html`

- Usecases:
    - Shared and central file system
    - Directory level restriction for roles is very useful if you want to restrict certain users in certain directory.

*Where to use EFS volumes and where to use EBS volumes*
- EFS can be mounted to multiple EC2 instances.
- EBS can only be mounted to a single EC2 instance.


### Lambda ###
- Lambda scales out automatically.
- Lambda functions are independent. 1 event = 1 function. 1 event = X number of lambda functions
- Lambda is serverless.
- Lambda timeout is 5 minutes.
**What AWS services are serverless?**
**What different languages are available for lambda?**
**What are the AWS Triggers?**
    - API Gateway
    - AWS IoT
    - Alexa Skills Kit
    - Alexa Smart Home
    - CloudFront
    - CloudWatch Events
    - CloudWatch Logs
    - CodeCommit
    - Cognito Sync Trigger
    - DynamoDB
    - Kinesis
    - S3
    - SNS


### Serverless Web ###
