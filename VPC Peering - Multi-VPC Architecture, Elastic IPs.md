<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-peering)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## VPC Peering

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated network in the AWS CLoud and it is useful because I can launch resources securely like servers. This resources can be set to be accessed within the VPC only or outside the VPC through the internet.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a connection between two VPC's using VPC peering. I test the connection by using a Ping command that send an ICMP traffic to the other VPC server. A reply coming from the server means a connection have been set up properlu.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was we can connect a VPC to each other and at the same time we can access resources from other VPC's by using VPC peering.

### This project took me...

This project took me one hour to finish.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two VPC's, I will use the VPC resource map to create VPC faster.

### Step 2 - Create a Peering Connection

In this step, I will set up a connection link between the two VPC using the VPC peering this will serve as a direct connection between the two VPC's.

### Step 3 - Update Route Tables

In this step, I will update my route tables so that traffic can enter MyVPCLab coming from VPCLab-2 and for traffic can enter VPCLab-2 coming from MyVPCLab.

### Step 4 - Launch EC2 Instances

In this step, I will create EC2 instance for each VPC to test the peering connection between the two VPC's.

---

## Multi-VPC Architecture

I started my project by launching two VPC's with different CIDR block so that when I need to use VPC peering the CIDR block will not overlap with each other

The CIDR blocks for VPCs 1 and 2 are for VPC 1 is 10.0.0.0/16 and for VPC 2 is 10.1.0.0/16. They have to be unique because during VPC peering the CIDR block of each VPC must be different to avoid routing conflicts and connectivity issues

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as we directly connect to the EC2 instance using the EC2 instance connect where it directly manages the Key Pairs.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is where to VPC are directly connected to each other and using their private IP address.

VPCs would use peering connections to directly connect two VPC using their private IP address. This means that data can now be transffered to the other VPC without using The Internet.

The difference between a Requester and an Accepter in a peering connection is the Requester is the one who request a connection to the other VPC and the Accepter is the one who accepts to establish a connection between the two VPC's.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because route tables will serves as routes so that traffic from the MyVPCLab will use the peering connection to access VPCLab-2. Route tables also serve as a way for trafic that enters the other VPC to access the resources inside that VPC.

My VPCs' new routes have a destination of the CIDR block of the other VPC. The routes' target was the created peering connection between the two VPC's.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 intance connect to access my EC2 instance directly without managing key pairs which are managed by AWS.

### Step 6 - Connect to EC2 Instance 1

In this step, I will access my EC2 instance using the EC2 instance connect now that my EC2 is now associated with a Public IPv4 address which is now used as a destination to access the instance.

### Step 7 - Test VPC Peering

In this step, I will ping the EC2 instance inside the VPCLab-2 using the EC2 instance inside the MyLabVPC to test the connectivity of the VPC peering.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to access my EC2 Intance directly in AWS management Console where key pairs are managed by AWS.

I was stopped from using EC2 Instance Connect as the EC2 intance does not have a public IPv4 address which is used as the target destination when accessing the ec2 instance.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static public IP address that we can request for our AWS account. Static IP address which we can allocate for an EC2 instance that even when rebooting the instance, the IP address will not change.

Associating an Elastic IP address resolved the error because a Public IPv4 address have been associated with the EC2 instance for the EC2 instance connect to work.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command "ping along with the private IPv4 address of the EC2 instance of other VPC". Ping is used to send a message to the IPv4 address  and waits a reply to check if a connection have been established.

A successful ping test would validate my VPC peering connection because we receive a reply coming from the receiver. Which proves that a connection between the two VPC's have been set up properly.

I had to update my second EC2 instance's security group by adding an inbound rule that allows ICMP traffic coming in from an specific CIDR block this includes the EC2 instance from the other VPC.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-peering_7a29d352)

---

---
