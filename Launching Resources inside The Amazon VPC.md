<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-ec2)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## Launching VPC Resources

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a logically isolated network inside your AWS Cloud and it is useful because you can launch your resources inside this network e.g., launching a EC2 instance and it can be private for security reasons and at the same time launch a new EC2 instance for public access.

### How I used Amazon VPC in this project

I used Amazon VPC to launch two EC2 instance server one for public access and for private which can only be accessed onside the VPC. I also created a new VPC using the option "VPC and more" which I can define the components inside my VPC and view the resource map without even creating it.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that I can create a VPC and also with it components at the same time. I can view the resource map before it is even created

### This project took me...

This project took me 1 hour to complete.

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means logging in and directly managing the virtual machine like it is infornt of you but over the internet.

### SSH is a key method for directly accessing a VM

SSH traffic means it is a protocol used to securely accessed a virtual machine it verifies the key to be fully authenticated to access the virtual machine. It encrypts traffic communication/data that is being transfered.

### To enable direct access, I set up key pairs

Key pairs help engineers/developers authenticate themselves to access their virtual machines e.g., Amazon EC2 instance. Key pair works with two private keys, one for the VM and a matching key for engineers/developers. 

A private key's file format is crucial so that different servers can read and process these private keys. My private key's file format was .pem privacy enhanced mail, is a go to for managing crypthographic keys and it is supported by many types of servers.

---

## Launching a public server

I had to change my EC2 instance's networking settings by changing the VPC and the subnet my EC2 instance was going to be launced in I updated both to my own VPC and  public subnet.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because it must be kept private only specific traffic can access the private server and it can not be accessed through the internet

My private server's security group's source is MyLab_SecurityGroup which means only those traffic that are allowed can access my private server.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I used the "VPC and more" options which allows me to create subnets, define how many availability zones are inside my VPC, and route tables all in one clicked. 

A VPC resource map is a visual diagram of the components inside my VPC how and where of each components are connected e.g., a public route table is connected to the Internet Gateway.

My new VPC has a CIDR block of 10.0.0.0/16 It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because every VPC created is not yet connected to the existing VPC and the CIDR block will not overlap with the existing VPC. VPC are isolated from each other but it is better for each VPC to have different CIDR because this needed for VPC peering.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options either none or one of each Availability Zones. This was because I only have 2 Availability Zones if I use all 3 Availability Zones then I will have 3 public sunets

The set up page also offered to create NAT gateways, this allows the connection between my private subnet and the internet. This allows outbound traffic from my private subnet to access the internet. e.g., if a resource needs to get update or data that is only available through the internet.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-ec2_8ee57662)

---

---
