# DNS 101 #
**Elastic Load Balancer doesn't have a IPv4 or IPv6 addresses, it only has a DNS name**

There are 2 types of DNS:
- Top level domain names: the last word in a domain name
    - .com
    - .edu
    - .gov
- Second level domain names: the second last word in a domain name
    - .co.XX
    - .gov.XXX
    - .com.XX

Database of all domain names
* `http://www.iana.org/domains/root/db`


# SOA Records #
SOA Record contains the details about a domain name and its owner.
- The name of the server that supplied the data for the zone.
- The administrator of the zone.
- The current version of the data file.
- The number of seconds a secondary name server should wait before checking for updates.
- The number of seconds a secondary name server should wait before retrying a failed zone transfer.
- The maximum number of seconds that a secondary name server can use data before it must either be refreshed or expire.
- The default number of seconds for the time-to-live file on resource records.


# NS (Name Server) Record #
NS Records are used by Top Level Domain servers to direct traffic to the Content DNS server which contains the authoritative DNS records.


# A Record #
An "A Record" is the fundamental type of DNS record and the "A" in "A Record" stands for "Address".
The "A Record" translates the name of the domain to the IP address.
    e.g. `blog.dnsimple.com.     A       185.31.17.133`


# CNAMES: Canonical Name #
CNAMES resolves one domain name to another domain name, instead of an IP.
For example, you may have a mobile website with the domain name http://m.cloud.guru for your mobile users. You may also want the name http://mobile.cloud.guru to resolve to this same address.
`mobile.cloud.guru      CNAME       m.cloud.guru`
`m.cloud.guru           A           185.31.17.133`

A CNAME record represents an alias for the target name and inherits its entire resolution chain.
Another example: blog.dnsimple.com as a CNAME of aetrion.github.io, which in turns is itself a CNAME of github.map.fastly.net, which is an A Record pointing to 185.31.17.133. In short terms, this means that blog.dnsimple.com resolves to 185.31.17.133.

`blog.dnsimple.com          CNAME       aetrion.github.io`
`aetrion.github.io          CNAME       github.map.fastly.net`
`github.map.fastly.net      A           185.31.17.133`


# Alias Records #
Alias records are used to map Resource Record Sets in your hosted zone to Elastic Load Balancers, CloudFront distributions, or S3 buckets that are configured as websites.
Alias records work like a CNAME record in that you can map one DNS name (www.example.com) to another target DNS name (elb1234.elb.amazonaws.com).

The key difference between a CNAME and Alias Record is, a CNAME can't be used for naked domain names (without www / zone apex record). You can't have a CNAME for http://cloud.guru, it must be an A Record or an Alias.

Naked domain must be an A Record, it can not be a CNAME.

Since you always need an IP address for your naked domain name, It causes problem with Route-53, because you can't get an IPv4 address of an Elastic Load Balancer. Because of that you can't create an A Record mapping your domain name with the ELB (A Record always maps to an IP). You can use the Alias Record, which can map your naked domain name to an ELB. And Amazon monitors and reflects underneath IP address of ELB (because the IP of ELB always changes and you don't have to maintain it in Route53).

**CNAME resolving is charged in AWS, but Alias Record resolving is free**


# TTL: Time To Live #
TTL is the length of time (in seconds) that a DNS record is cached on either the Resolving Server or the users own local PC. Once the TTL is expired your PC will look for the current DNS name. The lower the TTL is, the faster changes to DNS records take to propagate throughout the internet.



# Route 53 LAB #
Route 53 is a Global service.

- London Elastic Load Balancer
    - London WebServer 1
    - London WebServer 2
- Sydney Elastic Load Balancer
    - London WebServer 1

Different routing policies:
- Simple (default):
    - In a single region traffic will be distributed to all the machines equally.
    - User -> DNS Server -> EC2 (in your region).
    - Create a new record (an Alias record) of Simple Routing Policy pointing to London ELB as Alias Target.
- Weighted:
    - Traffic will be distributed to regions based on predefined weight of each region.
    - User -> DNS Server -> (based on the weight rule it divides traffic) -> Either London or Sydney ELB.
    - Create a new   record (an Alias record) of Weighted Routing Policy pointing to London ELB as Alias Target. Give the Weight 70
    - Create another record (an Alias record) of Weighted Routing Policy pointing to Sydney ELB as Alias Target. Give the Weight 30
- Latency:
    - Traffic will be distributed among Regions based on the lowest latency.
    - User -> Route53 -> (either) London | Sydney region
    - Create a new   record (an Alias record) of Latency Routing Policy pointing to London ELB as Alias Target and also specify the region.
    - Create another record (an Alias record) of Latency Routing Policy pointing to Sydney ELB as Alias Target and also specify the region.
- Failover:
    - Traffic will be routed based on the status (live/dead) of a region. You need to define Active and Passive (failover) regions.
    - User -> Route53 -> London (if live) | Sydney (if London is dead)
    - You need to define 2 health-checks on Route53,
        - one is for Primary region (ELB London).
        - another is for the entire domain (naked domain).
    - Create a new   record (an Alias record) of Failover Routing Policy pointing to London ELB as Alias Target, Mark it as Primary   FailoverRecordType and also associate it with London ELB health-check.
    - Create another record (an Alias record) of Failover Routing Policy pointing to Sydney ELB as Alias Target, Mark it as Secondary FailoverRecordType, here we don't need to associate it with any health-check.
- GeoLocation:
    - Traffic will be routed based on the user's geo-location.
    - Create a new   record (an Alias record) of GeoLocation Routing Policy pointing to London ELB as Alias Target and also specify Location to Europe.
    - Create another record (an Alias record) of GeoLocation Routing Policy pointing to Sydney ELB as Alias Target and also specify Location to Default (for all the other traffic).


# Exam Tips #
- Difference between Alias Record and a CNAME
- Prefer Alias Record over CNAME if you need to resolve it to AWS resource. Alias Record is free of cost but CNAME is not.
- Different routing policies.
    - Simple:
    - Weighted: A & B testing.
    - Latency: for quickest service
    - Failover:
    - GeoLocation:
