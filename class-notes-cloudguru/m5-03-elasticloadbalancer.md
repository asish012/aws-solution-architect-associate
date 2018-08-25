### Load balancer ###
- VM balances load across bunch of web servers.
- Application load balancer (OSI layer 7: HTTP/HTTPS)
- Network load balancer (OSI layer 4: TCP)
- Classic load balancer (old Elastic Load Balancer ELB)
    - Usually works on layer 4, but can also be configured (with x-forwarded-for) to work on layer 7.

* X-Forwarded-For Header: Your load balancer forwards the public ipv4 ip address of the original request to the WebService instance on your cloud.

* Error 504: The gateway timeout error. Underneath application is not responding, so the loadbalancer sends 504 to the user on timeout.


### Load balancer Lab ###
* One Subnet = One AZ

* For Elastic Load Balancer/Application Load Balancer you won't get a public ip address. You will only get a DNS name. IP for ELB is maintained by Amazon itself because it changes time to time.

- Creating a load balancer:
    - Provide the health check html page to ping
    - Number of failed requests before marking an instance out of service.
    - Time interval between requests.
    - Number of successful request before marking the instance live again.

**Read ELB FAQ**
