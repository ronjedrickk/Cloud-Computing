<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/hopeful_maroon_innocent_loquat/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is logically isolated network located at the AWS Cloud and it is useful because allows you to manage your own resources securely and in private.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a route tables, subnet, security groups, and Network ACLs.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was.

### This project took me...

This project took me an hour to complete this project.

---

## Route tables

Route tables are are like GPS that directs traffic to their destination inside the VPC.

Routes tables are needed to make a subnet public because it allows the connection between my VPC and the internet. The services inside my VPC can be accessed by the internet if the subnet is public.

![Image](http://learn.nextwork.org/hopeful_maroon_innocent_loquat/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which mean a destination is the IP address range a traffic must reach and target is the path a traffic needs to take to get to its destination.

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0..0.0.0/0 all IP address and a target of my Internet Gateway that is associated with my VPC

![Image](http://learn.nextwork.org/hopeful_maroon_innocent_loquat/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are like security guards that monitor/restricts traffic coming in and out of the resource, security groups are attach to a AWS resource.

### Inbound vs Outbound rules

Inbound rules are rules that control traffic/data that are going inside the resource. I  configured an inbound rule that allows HTTP traffic comming from an IP address range of 0.0.0.0/0.

Outbound rules are rules that control traffic/data that are going out of the resource. By default, my security group's outbound rule allows all traffic from any IPv4 address.

![Image](http://learn.nextwork.org/hopeful_maroon_innocent_loquat/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are are like traffic cops that operates the subnet level they monitor traffic that enter and exit my Network.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is set at a broad traffic rule and operates at the subnet level. Security Groups operates at the resource level and checks traffic going in and out at every resource.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all traffic.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all traffic.

![Image](http://learn.nextwork.org/hopeful_maroon_innocent_loquat/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---
