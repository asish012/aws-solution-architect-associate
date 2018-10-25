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

**Logs**
- _VPC Flow Logs_
    - VPC Flow Logs captures IP traffic going to and from network interfaces in your VPC. Flow log data is stored using Amazon CloudWatch Logs.
    - You can create a flow log for a VPC, a subnet, or a network interface.
- __