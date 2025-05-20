# VPC

Imagine you want to set up a private, secure, and isolated area in the cloud where you can run your applications and store your data. This is where a VPC comes into play.

A VPC is a virtual network that you create in the cloud. It allows you to have your own private section of the internet, just like having your own network within a larger network. Within this VPC, you can create and manage various resources, such as servers, databases, and storage.

Think of it as having your own little "internet" within the bigger internet. This virtual network is completely isolated from other users' networks, so your data and applications are secure and protected.

Just like a physical network, a VPC has its own set of rules and configurations. You can define the IP address range for your VPC and create smaller subnetworks within it called subnets. These subnets help you organize your resources and control how they communicate with each other.

To connect your VPC to the internet or other networks, you can set up gateways or routers. These act as entry and exit points for traffic going in and out of your VPC. You can control the flow of traffic and set up security measures to protect your resources from unauthorized access.

With a VPC, you have control over your network environment. You can define access rules, set up firewalls, and configure security groups to regulate who can access your resources and how they can communicate.

![image](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/12cc10b6-724c-42c9-b07b-d8a7ce124e24)

By default, when you create an AWS account, AWS will create a default VPC for you but this default VPC is just to get started with AWS. You should create VPCs for applications or projects. 

## VPC components 

The following features help you configure a VPC to provide the connectivity that your applications need:

Virtual private clouds (VPC)

    A VPC is a virtual network that closely resembles a traditional network that you'd operate in your own data center. After you create a VPC, you can add subnets.
Subnets

    A subnet is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC.
IP addressing

    You can assign IP addresses, both IPv4 and IPv6, to your VPCs and subnets. You can also bring your public IPv4 and IPv6 GUA addresses to AWS and allocate them to resources in your VPC, such as EC2 instances, NAT gateways, and Network Load Balancers.

Network Access Control List (NACL)

    A Network Access Control List is a stateless firewall that controls inbound and outbound traffic at the subnet level. It operates at the IP address level and can allow or deny traffic based on rules that you define. NACLs provide an additional layer of network security for your VPC.
   
Security Group

    A security group acts as a virtual firewall for instances (EC2 instances or other resources) within a VPC. It controls inbound and outbound traffic at the instance level. Security groups allow you to define rules that permit or restrict traffic based on protocols, ports, and IP addresses.  

Routing

    Use route tables to determine where network traffic from your subnet or gateway is directed.
Gateways and endpoints

    A gateway connects your VPC to another network. For example, use an internet gateway to connect your VPC to the internet. Use a VPC endpoint to connect to AWS services privately, without the use of an internet gateway or NAT device.
Peering connections

    Use a VPC peering connection to route traffic between the resources in two VPCs.
Traffic Mirroring

    Copy network traffic from network interfaces and send it to security and monitoring appliances for deep packet inspection.
Transit gateways

    Use a transit gateway, which acts as a central hub, to route traffic between your VPCs, VPN connections, and AWS Direct Connect connections.
VPC Flow Logs

    A flow log captures information about the IP traffic going to and from network interfaces in your VPC.
VPN connections

    Connect your VPCs to your on-premises networks using AWS Virtual Private Network (AWS VPN).
Here's a clear breakdown of the differences between:

---

## 🔄 NAT Gateway vs Transit Gateway

| Feature               | **NAT Gateway**                                     | **Transit Gateway**                                         |
| --------------------- | --------------------------------------------------- | ----------------------------------------------------------- |
| **Purpose**           | Allow **private** instances to access the internet  | Central hub for connecting **multiple VPCs & on-prem**      |
| **Use Case**          | Outbound internet access from private subnets       | Scalable network routing between VPCs, VPNs, Direct Connect |
| **Direction**         | Only supports **outbound** traffic                  | Supports **bi-directional** routing                         |
| **Applies To**        | Private EC2 instances (usually in a private subnet) | Multiple VPCs, on-prem networks, VPNs                       |
| **Internet-bound?**   | Yes (egress only)                                   | Not necessarily (routing only)                              |
| **Billing**           | Per GB and per-hour charge                          | Higher cost, charged by attachments and data processed      |
| **Availability Zone** | AZ-specific (one per AZ or highly available config) | Region-wide; scales across AZs                              |

### 🌐 Example:

* **NAT Gateway**: A private EC2 instance in a subnet without a public IP wants to update software via the internet.
* **Transit Gateway**: You have 5 VPCs and 1 on-prem data center; you want all to communicate efficiently through a central router.

---

## 🔐 NACL vs Security Group (with example)

| Feature                    | **Network ACL (NACL)**                                 | **Security Group**                                    |
| -------------------------- | ------------------------------------------------------ | ----------------------------------------------------- |
| **Applies To**             | Subnets                                                | EC2 instances (ENIs)                                  |
| **Stateless**              | ✅ Yes – you must define inbound **and** outbound rules | ❌ No – stateful (responses are automatically allowed) |
| **Rule Evaluation**        | Rules are processed **in order**                       | Rules are **evaluated all together**                  |
| **Default Action**         | Explicit **deny** if no rule matches                   | Implicit **deny** if no rule matches                  |
| **Supports Allow & Deny?** | ✅ Yes                                                  | ❌ Only **Allow**                                      |
| **Granularity**            | Coarser (applies to whole subnet)                      | Finer (applies to specific EC2 instance or ENI)       |

### 📌 Example:

#### NACL:

You want to **block** all traffic from a malicious IP to a subnet:

```text
Rule #100 | Deny | Source IP: 203.0.113.1 | Port: ALL | Protocol: ALL | Direction: Inbound
```

#### Security Group:

You want to allow **only port 22 (SSH)** to an EC2 instance from your office IP:

```text
Type: SSH | Protocol: TCP | Port: 22 | Source: 198.51.100.0/32
```

---

### 🔑 Key Takeaways:

* Use **NAT Gateway** for **internet access from private subnets**.
* Use **Transit Gateway** for **connecting multiple VPCs and networks**.
* Use **NACLs** for **broad subnet-level control**, especially when you need **deny rules**.
* Use **Security Groups** for **instance-level control**, especially when you want **stateful, easy-to-manage rules**.

Let me know if you want architecture diagrams for these.


## Resources 

VPC with servers in private subnets and NAT

https://docs.aws.amazon.com/vpc/latest/userguide/vpc-example-private-subnets-nat.html

![image](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/89d8316e-7b70-4821-a6bf-67d1dcc4d2fb)



