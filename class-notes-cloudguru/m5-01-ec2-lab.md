> 31 - 32

# Elastic Compute Cloud (EC2) - Lab #
We are going to setup our own EC2 (T2 micro free tier) instance.

**Configure EC2 Instance**
- Number of instances:
- Purchasing option: You can request for a Spot instance by bidding.
- Network: Select the VPC you want to use.
- Subnet: Availability Zone
- Auto-assign public IP:
- IAM role:
- Shutdown behavior:
- Monitoring: Using CloudWatch
- Tenancy: Dedicated | Shared
- Advanced - User data:
    - Bootstrap your instance:
        - instruct your instance to download and install apache/php/...
        - startup some service (e.g. apache)

- Storage:
    - Specify the root volume and its size, type etc.
    - Default: the Root volume is deleted on termination of your EC2 instance.
    - By default EBS root volume provided by amazon is not encrypted.
    - EBS Root volume can be encrypted using third party tools or if you create your own EBS from the AWS console or using API.

- Add tags:

- Security Group (virtual firewall):
    - You can specify SSH, HTTP, HTTPS, etc traffic to reach your instance.
    - You can specify the source from where the traffic should come from.


# Connect to your EC2 via SSH #
- First protect the key-pair of your EC2
    `chmod 400 EC2KeyPair.pem`

- SSH to your EC2
    `ssh ec2-user@54.173.10.61 -i EC2KeyPair.pem`

- Update newly created EC2
    `sudo su`
    `yum update -y`

- Install apache web server and create index.html
    `yum install httpd`
    `cd /var/www/html/`
    `vim index.html`
    `service httpd start`

- You should be able to see the web page using the public ip address of your EC2.

- Status Check of EC2 on aws console:
    - System Status Checks: Checks if the underlying hypervisor is up and running on AWS infrastructure.
    - Instance Status Checks: Checks if your instance can receive traffic.
