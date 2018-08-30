### Network ID, Subnet Mask & CIDR ###
Subnet Mask is also known as:
- Subnet Mask
- Network Mask
- Subnet ID
- Network ID

- Leaving out the subnet mask bits, the other bits are used for Host IDs.
- Putting 1 in all the subnet mask bits and 0 in all host bits then bitwise-or with the ip address gives you the network id.
    - IP with CIDR  : 192.168.40.55/21, which means 21 bits are for subnet-mask, and other 11 bits for host addresses.
    - IP in bits    : 11000000.10101000.00101000.00110111 (192.168.40.55)
    - Subnet mask   : 11111111.11111111.11111000.00000000 (255.255.248.0)
    - Network ID    : 11000000.10101000.00101000.00000000 (192.168.40.0)

Among the available Host IDs, one is reserved for the Router IP, and another one is reserved for Broadcast IP. The remaining IDs are the usable number of host ip addresses.
* Broadcast IP: The top ID (max ip) from the Host IDs

**Example 1**
IP Address with CIDR: 192.168.40.55/21 - What is the Network ID?
From the CIDR notation (/21) we can see the Subnet Mask is: 255.255.248.0 (11111111.11111111.11111000.00000000)

Subnet Mask : 11111111.11111111.11111000.00000000 (255.255.248.0)
IP Address  : 11000000.10101000.00101000.00110111 (192.168.40.55)
Network ID  : 11000000.10101000.00101000.00000000 (192.168.40.0)
Host ID     : 00000000.00000000.00000000.00110111 (0.0.0.55)

Available number of Host IDs            : 2^11 = 2048 IP Addresses
Available number of Host IP addresses   : 2048 - 1 (Max Host ID is reserved for Broadcast)
Broadcast address                       : 00000000.00000000.00000111.11111111 = 0.0.7.255
From the remaining IDs one is usually assigned for Router. And the remaining 2046 (2048 - 1 - 1) are available number of host IP addresses.

**Example 2**
IP Address with CIDR: 192.168.45.55/26 - What is the Network ID?
From the CIDR notation (/26) we can see the Subnet Mask is: 255.255.255.192 (11111111.11111111.11111111.11000000)

Subnet Mask : 11111111.11111111.11111111.11000000 (255.255.255.192)
IP Address  : 11000000.10101000.00101101.00110111 (192.168.45.55)
Network ID  : 11000000.10101000.00101101.00000000 (192.168.45.0)
Host ID     : 00000000.00000000.00000000.00110111 (0.0.0.55)

Available number of Host IDs            : 2^6 = 64 IP Addresses
Available number of Host IP addresses   : 64 - 1 (Max Host ID is reserved for Broadcast)
Broadcast address                       : 00000000.00000000.00000000.00111111 = 0.0.0.63
From the remaining IDs one is usually assigned for Router. And the remaining 62 (64 - 1 - 1) are available number of host IP addresses.

**Example 3**
IP Address with CIDR: 192.168.42.55/21 - What is the Network ID?
From the CIDR notation (/21) we can see the Subnet Mask is: 255.255.248.0 (11111111.11111111.11111000.00000000)

Subnet Mask : 11111111.11111111.11111000.00000000 (255.255.248.0)
IP Address  : 11000000.10101000.00101010.00110111 (192.168.42.55)
Network ID  : 11000000.10101000.00101000.00000000 (192.168.40.0)
Host ID     : 00000000.00000000.00000010.00110111 (0.0.2.40)

Available number of Host IDs            : 2^11 = 2048 IP Addresses
Available number of Host IP addresses   : 2048 - 1 (Max Host ID is reserved for Broadcast)
Broadcast address                       : 00000000.00000000.00000111.11111111 = 0.0.7.255
From the remaining IDs one is usually assigned for Router. And the remaining 2046 (2048 - 1 - 1) are available number of host IP addresses.

**Example 4**
IP Address with CIDR: 202.10.133.11/24 - What is the Network ID?
From the CIDR notation (/24) we can see the Subnet Mask is: 255.255.255.0 (11111111.11111111.11111111.00000000)

Subnet Mask : 11111111.11111111.11111111.00000000 (255.255.255.0)
IP Address  : 11001010.00001010.10000101.00001011 (202.10.133.11)
Network ID  : 11001010.00001010.10000101.00000000 (202.10.133.0)
Host ID     : 00000000.00000000.00000000.00001011 (0.0.0.11)

Available number of Host IDs            : 2^8 = 256 IP Addresses
Available number of Host IP addresses   : 256 - 1 (Max Host ID is reserved for Broadcast)
Broadcast address                       : 00000000.00000000.00000000.11111111 = 0.0.0.255
From the remaining IDs one is usually assigned for Router. And the remaining 254 (256 - 1 - 1) are available number of host IP addresses.


**IPv4 Classes**
| Class    | 1st Octet range       | Default Mask  |
| -------- | --------------------- | ------------- |
| Class A  | 1 - 126               | 255.0.0.0     |
| Class B  | 128 - 191             | 255.255.0.0   |
| Class C  | 192 - 223             | 255.255.255.0 |
|          |                       |               |
| Loopback | 127                   |               |
| Class D  | 224 - 239             | Multi-casting |
| Class E  | 240 - 255.255.255.254 | Experimental  |
