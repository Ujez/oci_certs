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

