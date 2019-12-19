# API Gateway #

**Following are valid integration source of API Gateway**
- Lambda 
- HTTP
- Mock
- AWS Service
- VPC Link

*On-premises APIs can integrated with AWS API Gateway through VPN Link and DirectConnect*

*You can enable caching to reduce the number of calls made to the endpoint and thus improve the latency*

**Throttle API Requests**
- To prevent your API from being overwhelmed by too many requests.
- API Gateway sets a limit on a steady-state rate and a burst of request
- Upon exceeding the limit AWS returns '429 Too Many Requests' error responses to the client
- API Gateway provides two basic types of throttling-related settings
    - Server-side throttling limits: are applied across all clients
    - Per-client throttling limits:
+ Throttling rate (default):
    - steady-state request: 10,000 requests per second
    - burst limit: 5,000 requests across all APIs within an AWS account

**AWS API Gateway protects your backend systems against DDoS attack**

**Debugging API access**
- Enable Access Logging: it includes errors and execution trace (request/response params, payloads)
- Enable CloudWatch Loggs: 


