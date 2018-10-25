# SQS: Simple Queue Service #
SQS is a distributed message queue service. It stores messages while waiting for a computer to process them.
Using Amazon SQS, you can decouple the components of an application so they run independently.

**Characteristics:**
- Pull based system
- Messages can be up to 256 KB of text in any format.
- Messages can be kept in the queue from 1 minute to 14 days.
- Default retention period is 4 days.
- Messages are processed at-least once.
- Any component of a distributed application system can put messages in the queue.
- Any other component of the distributed system can pick that message up using SQS API.

**Queue Types**
- Standard Queue (default)
    - Best-effort ordering (delivered in the same order as the are sent to the queue).
    - No guarantied ordering.
    - Delivered at-least once.
- FIFO Queue
    - Guarantied ordering (First in First out).
    - 300 transactions per second.

**SQS Visibility Timeout**
- The visibility timeout is the amount of time that the message is invisible in the SQL queue after a reader picks up the message. It provides time for the computation unit to process the message. If the processing of the message is over within the visibility timeout, the message will then be deleted from the queue and the timeout is expired, otherwise the message will become visible again and another reader will be able to pick it up. (This could result in the same message being delivered twice)
- Default visibility timeout: 30 seconds. (increase it if your task takes >30 s to process).
- Maximum timeout 12 hours.

**SQS Long Polling**
A Way to retrieve messages from the SQS Queue. Regular short polling returns immediately (even if the queue is empty), long polling doesn't return until a message arrives in the queue, or times out.

Usual short polling keeps asking if there is a message to retrieve. Which increases number of requests to the queue and increases the cost.


# SWF: Simple Workflow Service #
SWF helps to coordinate task across distributed application components. It helps developers build, run, and scale background jobs that have parallel or sequential steps. Jobs represent invocations of various processing steps by executable code, web service calls, human actions, and scripts.

**Two components of SWF**
- Workflow Starter: An application that initiates a workflow. i.e. website when placing an order, or mobile app searching train schedule.
- Decider: Program that controls the coordination of tasks (i.e. their ordering, concurrency, and scheduling according to the application logic).
- Worker: Programs that interact with Amazon SWF to get tasks, process them, and return the results.

**SWF vs SQS**
* SWF is a task-oriented API
* SQS is a message-oriented API
- SWF: A task is assigned only once and monitors their progress thus never duplicated with rescue effort.
- SQS: Once the message visibility timeout expires, the task is visible again and another worker machine can pick it up. It increases the chance of doing the task again.
* SWF: Since SWF task doesn't have a timeout, there can be human interaction involved/introduced during designing.

*SWF Domain parameters are specified in JSON format.*


# SNS: Simple Notification Service #
SNS is a pub/sub messaging and mobile notifications service. Its a push messaging service.

SNS allows you to group multiple recipients using topics. Interested parties can subscribe to one or more topics and all the subscribers will receive an identical copy of the message (appropriately formatted).

SNS Targets:
- SMS
- EMail
- SQS
- HTTP Endpoint
- Lambda functions via SNS topic
- Other AWS Services

**SNS vs SQS**
- SNS: Push (broadcast)
- SQS: Pull

*SNS is mostly used along with CloudWatch and Auto Scaling*


# Elastic Transcoder #
Amazon Elastic Transcoder is media transcoding (converting) service. It is used to convert (or “transcode”) media files from their source format into versions that will playback on devices like smartphones, tablets and PCs.


# API Gateway #
API Gateway makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. You can create an API that acts as a “front door” for applications to access data, business logic, or functionality from your back-end services, such as workloads running on EC2, code running on AWS Lambda, or any web application.

**API Types**
- REST API (uses JSON)
- SOAP API (uses XML)

**Benefits:**
- Low cost & efficient.
- Scales effortlessly.
- Expose HTTPS endpoints to define a RESTful API.
- Serverlessly connect to services like Lambda & DynamoDB.
- Send each API endpoint to a different target.
- Track and control usage by API key.
- You can Throttle Requests to prevent attacks.
- Connect to CloudWatch to log all requests.

**How to configure API**
- Define an API.
- Define Resources and nested Resources (URL paths).
- For each resource:
    - Select supported HTTP methods. (GET | POST | DELETE | ...)
    - Set security.
- Deploy API to a stage

**API Caching:**
You can enable API caching in API Gateway to cache your endpoint's response. Caches lives a specified time-to-live (TTL) period.

**Same Origin Policy:**
A web browser permits scripts contained in a first web page to access data in a second web page, but only if both pages have the same origin.

**CORS: Cross-Origin Resource Sharing:**
CORS is a mechanism that allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from which the first resource was served.

CORS is one way the server at the other end (not the client code in the browser) can relax the same-origin policy.

* Error: "Origin policy cannot be read at the remote resource."
* Solution: You need to enable CORS on API Gateway.


# Kinesis #
Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information.
With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications.

**Kinesis Services**
- Kinesis Streams: Puts data into Shards (a temporal data storage), where you can apply your computations.
    * Kinesis Data Streams:
    * Kinesis Video Streams:
- Kinesis Firehose: Capture, transform, and load data streams into AWS data stores (S3) or ElasticSearch Cluster for near real-time analytics.
- Kinesis Analytics: Process data streams in real time with SQL.

Kinesis Streams stores data for 24 hours (default). You can extend it up to 7 days.


**Shard:**
Kinesis Streams puts the data into Shards.


# CloudFormation #
<!-- From Pluralsight AWS SA Professional -->
CloudFormation gives developers an easy way to create and manage a collection of related AWS resources, provisioning and updating them in an orderly and predictable fashion.

You can automate almost any services on AWS platform.
You can also find a lot of other third party CloudFormation scripts that you can download and can deploy complex environment. i.e. Citrix XenApp or Citrix XenDesktop environment.

**Components:**
- Templates: Architectural design, written in JSON.
- Stacks: Deployed set of AWS resources based on templates.

**Deployment:**
Once created we can deploy the CloudFormation template in 3 ways:
- Management Console
- CLI
- APIs

# CloudFormation - Templates #
**Template Elements:**
- Mandatory elements
    - File format and version
    - List of resources and associated configuration values
- Optional elements
    - Template parameters (max 60 params)
    - Output values
        - IP of an instance
        - DNS name of and ELB
        - Name of a VPC
        - ...
    - List of data tables (static values)
        - AMI names

**Intrinsic Functions:**
Build-in functions that help you manage the stacks. i.e.
- Fn::Base64
- Condition Functions
- Fn::FindInMap
- Fn::GetAtt
- Fn::GetAZs
- Fn::Join
- Fn::Select
- Ref

Example: Fn::GetAtt
- Declaration: "Fn::GetAtt" : [ "logicalnameOfResource", "attributeName" ]
- Example    : "Fn::GetAtt" : [ "ELB", "DNSName" ]

**Supported:**
- Puppet and Chef integration
- Bootstrap script
- Define deletion policies
- Provides WaitCondition
- Create roles in IAM
- VPCs can be created and customized
- VPC peering in the same AWS account
- Route 53

**Stack Creation Errors:**
On encountering and error by default CloudFormation is configured to rollback.


# KMS: Key Management Service #
<!-- Udamy AWS Developer -->
KMS makes it easy for you to create and control the encryption keys used to encrypt your data, and uses FIPS 140-2 validated hardware security modules to protect the security of your keys.
