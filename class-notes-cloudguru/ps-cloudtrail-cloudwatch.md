Elastic Load Balancer:
    Elastic Load Balancing automatically distributes your incoming application traffic across multiple targets (EC2/S3)
Route53
    Simple Routing
    Weighted Routing
    Latency Routing
    Failover Routing
    GeoLocation Routing
Auto Scaling Group
    Automatically scale-out or scale-in based on defined rules (high cpu usage, high traffic, etc)


### CloudTrail vs CloudWatch ###
**CloudTrail**
CloudTrail is a logging service. It logs everything that you do on AWS platform. Since AWS is API driven, CloudTrail monitors every API call that are made from Console, CLI, SDK, etc.

CloudTrail record includes:
- The identity of the API caller.
- Time of the API call.
- Source IP address of the API caller.
- Request parameters.
- Response elements returned by the AWS service.

These are not enabled by default. Can be enabled per region.

**CloudWatch**
CloudWatch is a monitoring service for AWS resources and applications. e.g. EC2 CPU usage and others.
It also has CloudWatch-Logs. Where you can receive and store CloudTrail Logs, and later you can filter based on keywords, and you can put matrices against these filters.

CloudWatch does:
- Collect and track matrices.
- Collect and monitor log files.
- Set alarms.
- Automatically react to changes in your AWS resources.

CloudWatch Logs:
- Logs will be stored indefinitely.
- Alarm history is stored for 14 days.
- CloudTrail logs can be sent to CloudWatch Logs for real-time monitoring.
- You can filter by specific terms, phrases, or values from CloudWatch Logs (including CloudTrail logs that are sent to CloudWatch Logs).
- You can set CloudWatch Alarms based on your filters.

**Storing Logs**
- CloudWatch Logs.
- Centralized logging system (Splunk).
- Custom script and store on S3.

**Monitoring**
- Don't store logs on non-persistent disks:
    - EC2 instances root volume
    - Ephemeral storage
- Best practice is to store logs in CloudWatch Logs or S3 buckets.
- CloudTrail can be used across multiple AWS accounts while being pointed to a single S3 bucket (requires cross account access).
- CloudWatch Logs subscription can be used across multiple AWS accounts (requires cross account access).


### Trusted Advisor ###
Free auditing service, where you can get AWS advises to help you reduce cost, increase performance, and improve security by optimizing your AWS environment.
It also provides real time guidance to help you provision your resources following AWS best practices.
