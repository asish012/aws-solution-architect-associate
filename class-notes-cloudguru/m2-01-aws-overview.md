### AWS global infrastructure ###
- Geographical regions
    - London, Berlin, NY, CA, ... ...
- Availability zone inside each region
    - At-least 2 availability zones per geographical region (aka. data centers)
- Edge location
    - For caching

* All the AWS services sits on top of AWS global infrastructure.

<!-- Set 1 -->
### AWS services: Compute ###
- EC2: Elastic Compute Cloud:
- EC2 Container Service: Runs docker containers.
- Elastic Beanstalk: (more important for developers and sysadmins): Run code on an infrastructure that is automatically provisioned to host that code.
- Lambda: Upload your code and control when it executes. Your lambda function will execute based on some events.
- Lightsail:
- Batch: (no exam questions)

### AWS services: Storage ###
- S3: Object based storage. Upload data into buckets.
- EFS: Elastic File System.
- Glacier: Data archiver.
- Snowball: Bring large amount of data in terabytes directly write into disks.
- Storage Gateway: VMs in data-centers that replicates data into S3.

### AWS services: Databases ###
- RDS: Relational database service.
- DynamoDB: Non-relational db.
- Elasticache: Query from db and cache.
- Red Shift: Built for data warehousing.

### AWS services: Migration ###
- AWS Migration Hub: Tracks and visualize the process and progress during migration to AWS from private server and integrate with other AWS services.
- Application Discovery Service: Applications and their dependencies.
- Database Migration Service:
- Server Migration Service:
- Snowball: It works as database service and also as migration service. Migrates large amount of data into AWS.

### AWS services: Networking and Content Delivery ###
- VPC: (IMPORTANT): Virtual data center. You can configure firewalls, availability zone, network side address ranges, network route table etc...
- CloudFront: Content delivery network.
- Route53: highly scalable DNS service
- API Gateway: (IMPORTANT): Create your own API for your other services.
- Direct Connect: (IMPORTANT): Directly connect your corporate network to AWS and directly connect to your VPC.

### AWS services: Developer Tools ###
<!-- Not very important for architect exam, but very important for developing -->
- CodeStar: Code management/project management/collaboration tool tool, includes contentious integration tools.
- CodeCommit: Source control (store your source), store your own private git repository within codecommit.
- CodeBuild: Compile your code.
- CodeDeploy: Automate code deployment to your EC2 instances or on premise instances or lambda functions.
- CodePipeline: Continuous delivery service and you can model and visualize and automate the steps to release your software.
- X-Ray: To debug and analyze your application, including requests tracing.
- Cloud9: IDE to write your code.

<!-- Set 2 -->
### AWS services: Management Tools ###
- CloudWatch: Monitoring tool.
- CloudFormation: (IMPORTANT): Way of scripting infrastructure architecture. Deploying zoomla/wordpress/sharepoint sites becomes easy.
- CloudTrail: (IMPORTANT): Logs all your activities in AWS environment. Turned-on by default and keeps logs for 1 week.
- Config: (IMPORTANT): Monitor your entire AWS environment.
- OpsWorks: Way of automating your environment via using "chef" and "puppet".
- Service Catalog: (no exam questions): Way of managing catalog of all IT services.
- Systems Manager: (no exam questions): Manage your AWS resources. Usually for EC2. If you want to install bunch of security patches across all your EC2 instances.
- Trusted Advisor: (IMPORTANT): Advises you to optimize your usage of AWS services, about security and other stuff.
<!-- Responsibility of Trusted advisor and Inspector is very important for associate exam -->
- Managed Services: (no exam questions)

### AWS services: Media Services (new service) (no exam questions) ###
- Elastic Transcoder:
- MediaConvert: File based video transcoding service. Create and broadcast multi-screen on-demand live video.
- MediaLive: Broadcast grade live video processing service. High quality video stream.
- MediaPackage: Protects your video.
- MediaStore: Storage service optimized for media.
- MediaTailor: Targeted advertising into your video stream.

### AWS services: Machine Learning (no exam questions) ###
- SageMaker: Deep learning.
- Comprehend: Understand what your user says about you.
- DeepLens: Artificially aware camera. Physical camera.
- Lex:
- Machine Learning: Analyze your own dataset.
- Polly: Text to Speech engine.
- Rekognition: Video and image recognition engine.
- Amazon Translate:
- Transcribe: Automatic speech recognition from video.
<!-- You want your own multi-lingual translator?
     User Transcribe to get the speech from a video, then use Translate to translate that to other language and then use Polly to convert that text into speech. -->

### AWS services: Analytics ###
- Athena: (no exam questions): Run SQL on your S3 buckets.
- EMR (Elastic MapReduce) (IMPORTANT): Processing BigData.
- CloudSearch:
- ElasticSearch:
- Kinesis: (IMPORTANT): Injecting big data into AWS environment. Used for collating large amounts of data streamed from multiple sources.
- Kinesis Video Streams:
- QuickSight: (no exam question): BI tool.
- Data Pipeline (IMPORTANT):
- Glue: ETL tool.

<!-- Set 3 -->
### AWS services: Security Identity and Compliance ###
- IAM: (IMPORTANT)
- Cognito: Way of device authentication.
- GuardDuty: (no exam question):
- Inspector: (IMPORTANT)
- Macie: Look for personally identifiable data in your bucket.
- Certificate Manager: Manage SSL certificate
- CloudHSM: (IMPORTANT): Hardware Security Module.
- Directory Service: Way of integrating Microsoft Directory Service
- WAF: (IMPORTANT): Web Application Firewall. Firewall on application layer.
- Shield: (IMPORTANT): Protect from DDos attack.
- Artifact:

### AWS services: Mobile Services (no exam questions) ###
- Mobile Hub: (no exam questions)
- Pinpoint:  (no exam questions): Targeted push notification.
- AppSync:
- Device Farm:  (no exam questions): Testing on real mobile devices.
- Mobile Analytics:  (no exam questions)

### AWS services: AR & VR (no exam questions) ###
- Sumerian

### AWS services: Application Integration ###
- Step Functions: (no exam questions)
- Amazon MQ: (no exam questions)
- SNS: Alert for AWS service usages/over-usages
- SQS: Simple Queue Service. Decoupling your infrastructure.
- SWF: Simple Work Flow.

### AWS services: Customer Engagement ###
- Connect: (no exam questions)
- Simple Email Service:

### AWS services: Business Productivity ###
- Alexa For Business: (no exam questions)
- Chime: Video conferencing.
- Work Docs:
- WorkMail: (no exam questions)

### AWS services: Desktop & App Streaming (no exam questions) ###
- Workspace:
- AppStream 2.0: Application streaming service. The app is running on AWS and streamed to your devices.

### AWS services: IoT (no exam questions) ###
- iOT:
- iOT Device Management:
- FreeRTOS:
- Greengrass:

### AWS services: Game Development (no exam questions) ###
- GameLift: Develop games.
