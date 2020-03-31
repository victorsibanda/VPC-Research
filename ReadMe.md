# VPC - Virtual Private cloud

It is a configurable pool of shared computing resources within a public cloud environment, such as AWS.
The use of VLAN allows for the isolation of one cloud user from either users of the same cloud and public cloud users.
VPC is most commonly used as IaaS.
AWS, IBM Cloud, Google Cloud Platform and Microsoft Azure all allow for the use of VPC'.s
192.168.0.0/16 can accommodate 65,534 different IP address as well as 256 different subnets.
You can only set this when you create your VPC as after creation there is no way to change your network block.

## What are subnets

There are different sizes of subnets which depends on connectivity and the technology.
- Point-to-point subnet allows two devices to connect
- data center subnet might be designed to connect many more devices

Subnets break large networks into smaller, more manageable networks that run more efficiently

each subnet is a logical subdivision of the bigger networks

connected devices within a subnet share a common IP address identifier - communications

Routers manage communication between Subnets

This allows IP address reallocation

Relieves network congestion

Better security
- subnet segmentation within an organisation stay local.

## Private and Public Subnets

- A Private Subnet is a subnet in which it instances only need private IP which mean there is no internet access unless you add the route 0.0.0.0/0.
- A public subnet routes 0.0.0.0/0 through an internet gateway. You would need a private IP to talk to the internet. 

# NACL's vs Security Groups

A Security Group is the firewall of an EC2 instance.

A Network Access Control List (NACL) is the firewall of the Subnet.

NACLs are applicable at the subnet level, so any instance in the subnet with an associated NACL will follow rules of NACL.

That’s not the case with security groups, security groups has to be assigned explicitly to the instance. This means any instances within the subnet group gets the rule applied.

If you have many instances, managing the firewalls using Network ACL can be very useful. Otherwise, with Security group, you have to manually assign a security group to the instances.

## Stateful vs Stateless

Security groups are stateful: This means any changes applied to an incoming rule will be automatically applied to the outgoing rule. e.g. If you allow an incoming port 80, the outgoing port 80 will be automatically opened.

Network ACLs are stateless: This means any changes applied to an incoming rule will not be applied to the outgoing rule. e.g. If you allow an incoming port 80, you would also need to apply the rule for outgoing traffic.

## Rules: Allow or Deny

Security group support allow rules only (by default all rules are denied). e.g. You cannot deny a certain IP address from establishing a connection.

NACL support allow and deny rules. By deny rules, you could explicitly deny a certain IP address to establish a connection example: Block IP address 123.201.57.39 from establishing a connection to an EC2 Instance.

## Defense order

Security group first layer of defence, whereas NACL is second layer of the defence.

# Network Access Controls

NACs are stateless, meaning that you need to set both the inbound and outbound rules separately

## APP

- port 80 - This is the port the HTTP GET request comes in on, when the browser asks to display
- port 443 - This port allows for HTTPS requests, requiring more security than a standard HTTP request that port 80 is used for.
- port 22 - This port is used to accept the SSH key into the app to authorise admin access.
- port 3000 - This port is generally used to run an app through NGINX or APACHE.
- port 8080 - This port is most commonly used for access to a web server (such as AWS) as a non-root (or non-admin) user


## DB

- port 1433 - This is the port most commonly used to access an MSSQL database server through TCP/IP. It's assumed that DB is connecting to APP through this port.
- port 22 - It's assumed that the DB is using port 22 to check the SSH access of a user.
- port 27017 - Alternative to 1433, MongoDB uses port 27017 to communicate.
