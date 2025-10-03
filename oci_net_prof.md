# VCN
A vcn IP should not overlap with another vcn.

## Subnet
A vcn is divided into subnets. Each subnets has a contiguous range of IPs described in CIDR notation. Subnet IP ranges cannot overlap. IPV6 is optional. A Subnet can grow or shrink after creation. Each subnet can be: `AD-specific`: containted in a single AD in a multi-AD region, can be `Regional(recommended)`: spans all 3 ADs in a multi-AD region.
VNICs determines how the instance connects with endpoints inside and outside the VCN.

## VNICs
Has an optional host name for DNS for each private IP addr. Also has a MAC addr. A flag to enable or disable the src/dst check on the VNIC's network traffic. NSG hv __security rules__ that apply on that apply only to the VNICs in that NSG. VNICs also have OCIDly to the VNICs in that NSG. VNICs also have OCID.
Every VNIC is assigned a primary private IP addr when it is created, which is configured automatically on the corresponding Ethernet device in the instance OS.
Every VNIC can have additional private IPs called secondary private IP(max 31).
A VNIC resides in a subnet and enables a compute instance to be connected to a VCN via route tables, and security rules determine connectivity of aht compute instance.

![](img/ad32.png)

### Private IP
Each instance has at least one primary private IP.
When a public subnet is used, a private IP can have an __optional__ public IP assigned to it.
Every VNIC has one primary IP and can have additional priv IPs called secondary private IPs.

![](img/ad33.png)

### Public IP
You can assign a given resrouce multiple public IPs across one or more VNICs.
They can be ephemeral or reserved.
When you launch an instance in a public subnet, by default, the instance gets a public IP unless you say otherwise.
After you create a given pulic IP, You cannot change its type. That is if you launch an instance that is assigned an ephemeral public IP with addr,lets say 1.11.1.1, you cannot convert the ephemeral public IP to a reservfeed public IP with addr 1.11.1.1.

![](img/ad34.png)

 There are also the concept of BYOIP, which has some strict rules that must be followed.

![](img/ad34.png)

__IP Pools__
What baffles me here is how OCI manages this...would they run out of ip addresses if customers are reserving large amounts of IPs.

![](img/ad37.png)

## Security Lists
Stateful Security Rules

![](img/ad38.png)

Stateless Security Rules

![](img/ad39.png)

On a final note, some protocols, like ICMP, require an egress rule regardless of the state option. 

## NSGs

![](img/ad40.png)

## OCI Gateway

### Internet Gateway
![](img/ad42.png)

IG provides a path for network traffic btw your VCN & the internet. Your can hv onl one IG per VCN. After creating an IG, you must add a route for the gateway in the public subnet route table to enable traffic flow. the IG allows inbound traffic to the pucli subnet. Instances need a public IP addr assigned.


![](img/ad41.png)

### NAT Gateway
Host can initiate outbound connections to the internet and recieve responses, but no receive inbound connections initiated from the internet. Uses case: Updates, patches.
Something that is distinct in the OCI is once your setup a NAT gateway you don't need to setup an IG for you to use the NAT Gateway

![](img/ad43.png)

Below is a figure showing the limits and boundaris for the NAT gateway.

![](img/ad44.png)

### Dynamic Routing Gateway(DRG)
some of the main features of DRG incs:

![](img/ad45.png)

however DRG has its special use cases:

![](img/ad46.png)

here are some DRG attachments

![](img/ad47.png)

### Remote Peering Connection(RPC)

### Service Gateway

![](img/ad49.png)

### Private Endpoints


![](img/ad48.png)

Below is Private endpoints in Object Storage

![](img/ad50.png)

### Public IPs
You can assign a public IP to an instance to enable communication with the internet.The instance is assigned a public IP from the OCI addr pool.
here are some things that must be put in place for the instance to comm directly with the internet:


![](img/ad51.png)

Public IPs come in two categories:


![](img/ad52.png)


__Ip address insight__- a cool tool in OCI i think you should checkout.

### Notes on LB
There are actually 2 categories:
http and Network LBs.
For the HTTP LBs, there is the _content-based routing: host based_ - involves multiple websites using a single LB & a independent set of back-end servers.

![](img/ad53.png)

There is another known as the path-based still under the content-based routing:

![](img/ad54.png)

There are two types of LBs:

![](img/ad55.png)

![](img/ad56.png)


__Load Balancing Policies__ 
A note on this use case:

You are tasked with configuring a Network Load Balancer (NLB) in Oracle Cloud Infrastructure (OCI) to distribute traffic among a group of backend servers. Your backend servers are hosting a critical application that requires session persistence based on both source and destination IP addresses, source and destination ports, and protocol. Which NLB configuration option should you select to meet this requirement?

_Answer_: 5-Tuple Hash: Routes incoming traffic based on 5-Tuple (source IP and port, destination IP and port, protocol) Hash. This is the default Network Load Balancer policy.

![](img/ad57.png)

## DNS Management
_read up on this_

## Traffic Steering
Traffic mgt enables customers to config routing policies for serving intelligent responses to DNS queries.
Different answers can be served for a query according to the logic in the customer-defined Traffic management Steering Policy, thus sending users to the most optimal location in your infra.
__Use cases__:

![](img/ad58.png)

Example: You are responsible for optimizing traffic flow in your Oracle Cloud Infrastructure (OCI) environment and want to implement Traffic Management Steering Policies to direct users to the nearest available instance. Which steering policy in Oracle Cloud Infrastructure Traffic Management should you choose for this purpose?

_Answer_: Geolocation Steering policies distribute DNS traffic to different endpoints based on the location of the end user.


__Traffic Mgt Concepts__:


![](img/ad59.png)

_checkout Geolocation traffic steering lab_

# Design for Hybrid Networking Architecture

## BGP

### Equal-Cost Multi-Path Routing(ECMP)

ECMP enables flow-based load balancing of network traffic over multiple virtual circuits or multiple IPsec tunnels (not a mix) using BGP.
It allows active-active LBing and failover of network traffic btw a maximum of 8 circuits.
5-tuple is used to distinguish flow. Multiple flows will be necessary to utilize all available bandwidth.


![](img/ad60.png)

An overview of an architecture for ECMP


![](img/ad61.png)

### Site-to-Site VPN
offers a simple & secure way to connect your corporate network to OCI over your existing internet connection. It is recommended to always use BGP for all your tunnels, or static routing for all your tunnels

![](img/ad62.png)


This are some of the use cases:

![](img/ad63.png)

Another method of connecting on-premise to OCI is through the following topic below 

### FastConnect
From the image below we would be focused on FastConnect

![](img/ad64.png)


![](img/ad65.png)

below are FastConnect connectivity models

![](img/ad66.png)

And then 