# AWS Security using Security Groups and NACL 

AWS (Amazon Web Services) provides multiple layers of security to protect resources and data within its cloud infrastructure. Two important components for network security in AWS are Security Groups and Network Access Control Lists (NACLs). Let's explore how each of them works:

    Security Groups:
        Security Groups act as virtual firewalls for Amazon EC2 instances (virtual servers) at the instance level. They control inbound and outbound traffic by allowing or denying specific protocols, ports, and IP addresses.
        Each EC2 instance can be associated with one or more security groups, and each security group consists of inbound and outbound rules.
        Inbound rules determine the traffic that is allowed to reach the EC2 instance, whereas outbound rules control the traffic leaving the instance.
        Security Groups can be configured using IP addresses, CIDR blocks, security group IDs, or DNS names to specify the source or destination of the traffic.
        They operate at the instance level and evaluate the rules before allowing traffic to reach the instance.
        Security Groups are stateful, meaning that if an inbound rule allows traffic, the corresponding outbound traffic is automatically allowed, and vice versa.
        Changes made to security group rules take effect immediately.
```
aws allow deafult all the outbound traffic (means your server can access anything from the internet) except 25 port beacuse there can be a lot of spam activity
Port 25 is the default port for sending email using SMTP (Simple Mail Transfer Protocol).

If AWS allowed unrestricted access to port 25, malicious users could use EC2 instances to send massive amounts of spam, phishing emails, or malware.

This would lead to:

Blacklisting of AWS IP addresses by major email providers (Gmail, Outlook, etc.)

Reputation damage to AWS's global infrastructure

Delivery problems for legitimate AWS customers
```

    Network Access Control Lists (NACLs):
        NACLs are an additional layer of security that operates at the subnet level. They act as stateless traffic filters for inbound and outbound traffic at the subnet boundary.
        Unlike Security Groups, NACLs are associated with subnets, and each subnet can have only one NACL. However, multiple subnets can share the same NACL.
        NACLs consist of a numbered list of rules (numbered in ascending order) that are evaluated in order from lowest to highest.
        Each rule in the NACL includes a rule number, protocol, rule action (allow or deny), source or destination IP address range, port range, and ICMP (Internet Control Message Protocol) type.
        NACL rules can be configured to allow or deny specific types of traffic based on the defined criteria.
        They are stateless, which means that if an inbound rule allows traffic, the corresponding outbound traffic must be explicitly allowed using a separate outbound rule.
        Changes made to NACL rules may take some time to propagate to all the resources using the associated subnet.

```
on the subnet level we can apply additional layer with the alllow we can also add what kind of traffic you can deny like 0.0.0.0 so that it does'nt affect or risk the security of your server unintentionaly
we cab use nacl for automation where instead of adding security to 100 server manually you can just at subnet level and it will apply to all the server
```

## Project Implemented in the video


![Screenshot 2023-06-29 at 12 14 32 AM](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/30bbc9e8-6502-438b-8adf-ece8b81edce9)

