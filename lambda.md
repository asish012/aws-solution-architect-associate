*When a lambda function reaches the maximum configured memory, it gets terminated with an error msg. Doesn't get timeout.*

**Lambda within a VPC+Subnet**
- Lambda functions can run within a private VPC with resources within a subnet
- In this case if you want the lambda to communicate with S3, you must use either Nat Gateway or S3 VPC endpoint with route-table configuration.
- Otherwise lambda gets timeout
**Lambda in a 'No VPC' mode**
- If a lambda runs in 'no VPC' mode, it won't have access to resources running in a private VPC

*Lambda function can reach to S3 bucket from another region as long as it has internet connection*

**Dead Letter Queue (DLQ)**
- You can configure to forward non-processed payloads to Dead Letter Queue using QSQ, SNS
- And process that (retry, send email, other notification, etc)
- Lambda alutomatically retries failed execution

**Non-persistent disk space limit**
- Each lambda function receives 500MB of non-persistent (ephemeral) disk space (/tmp directory)
- If your function needs to use space in disk then 512MB is the limit

**Receive trigger from CloudWatch**
- Through CloudWatch Rules you can trigger Lambda function. Two parts of CloudWatch Rule
    - Event Source: Event Pattern or Schedule
    - Target: You can select Lambda/SNS/SQS/KinesisStream/...
        - As Input you can pass the whole or partial matched event (as JSON) or constant data as JSON.


