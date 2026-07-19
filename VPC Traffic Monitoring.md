<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-monitoring)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is logically isolated network in the AWS Cloud where wen launch our own resources, and it is useful because we can properly secure our own resources using Network ACLs and Security Group. We can connect two VPC's to communicate with each other securely and privately using the VPC Peering and we can use VPC Flow Logs to view the traffic that enters our VPC with its source and destination.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to monitor incoming network traffic using VPC flow logs and Amazon CloudWatch Logs to store this records.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was we can view the network traffic flow in our VPC using VPC Flow logs and CloudWatch by saving the  network traffic records.

### This project took me...

This project took me one hour to finish.

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will set up to two VPC's using the VPC wizard, to launch the VPC in minutes. This includes route tables, subnets, Network ACLs, Security Groups, and Internet Gateway.

### Step 2 - Launch EC2 instances

In this step, I will launch an EC2 instance for each VPC that I created because I will be using these EC2 instance later when I need to check the connection betwen the two VCP's.

### Step 3 - Set up Logs

In this step, I will set up a way to track all inbound and outbound traffic and store this records because I will be using this records to analyze the network traffic in my VPC.

### Step 4 - Set IAM permissions for Logs

In this step, I will create an IAM Policy and Role that give VPC Flow Logs permission to write logs and send them to CloudWatch.

---

## Multi-VPC Architecture

I started my project by launching two VPC's with different CIDR blocks. They must have differnet CIDR blocks so that when I will use VPC peering later their IPv4 Address will not overlap and cause connectivity issues.

The CIDR blocks for VPCs 1 and 2 are 10.0.0.0/16 and 10.1.0.0/16. They have to be unique because I can't use VPC peering on VPC's with the same CIDR block, this will cause connectivity issues.

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow ICMP traffic from all IP address. This is because when I try to send a message using ICMP to check the connection. The security group will allow an ICMP traffic comming from the IP address.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are like diary in our computer that stores everything that happens in my computer. Which can be accessed when something happened in our computer or when we are troubleshooting.

Log groups are large folder in the AWS that keeps related logs together. Log groups are Region-specific which means that logs and data that is created in that Region are saved in that Region.

### I also set up a flow log for VPC 1

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy so that the resources are allowed to create log groups within CloudWatch and allows tha IAM role to send log data to the streams.

I also created an IAM role because we can assign the policy to a specific user or service in this AWS Account.

A custom trust policy isused to enable others to perform actions in an AWS account. This can be applied to an feature inside an AWS service, like VPC Flow Logs. Other services can't used the custom trust policy.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will test the connectivity between my VPC's. I wiil try to send a test message from my EC2 instance 1 to EC2 instance 2 in my other VPC.

### Step 6 - Set up a peering connection

In this step, I will set up a VPC peering connection between the two VPC's because with this feature, the two VPC can be directly connected and communicate without using the public Internet.

### Step 7 - Analyze flow logs

In this step, I will review and analyze the flow logs recorded in my VPC 1 subnet so that I know what network trafic are suspicious and what are the proper steps in handling this network traffic.

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means that there is no connection between the two VPC's or there is no routes that directs the ICMP traffic to the destination.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means that I can access the server publicly through the internet but this is not a best practice when accessing a EC2 instance.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because the two VPC's are not directly connected to each other. In this case we need to use VPC peering between the two VPC and set up a route table for each, so that the network traffic will have route to its destination.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables so that the network traffic comming from the other VPC will know it's way going to their intended destination.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means a connection have been etablished betwen the two VPC's.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about what have happened in my computer. This contains a message about the sender and whether the message is accepted or rejected.

For example, the flow log I've captured tells us me about message containing which AWS sent the message, the IPV4 Address, port number, bytes of the data sent and whether the traffic is accepted or rejected.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is is a feature in CloudWatch that helps analyze logs. It filters, process, and combine data to help troubleshoot the problem.

I ran the query "stats sum(bytes) as bytesTransferred by srcAddr, dstAddr
| sort bytesTransferred desc
| limit 10". This query analyzes the last ten bytes transfers based on source and destination IP addresses.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-monitoring_3e1e79a1)

---

---
