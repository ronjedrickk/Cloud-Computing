<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-connectivity)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## Testing VPC Connectivity

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is logically isolated network in My AWS Cloud and it is useful because I can launch resources inside this network securely, I can make these resources private or publicly accessible. I set up its own traffic rules, route tables, Network ACLs, security groups, and Internet Gateway.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to to test connectivity between a public server and private server using ping command and adding ICMP rules to my Network ACLs and Security Groups. Test if  my Public server is connected through the internet by using curl command. Curl is used to retrieve an HTML data from a public server using the command curl followed by the website address.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was I there is a more direct, easier, and secure way to access a VM/Server other than using SSH with key pairs

### This project took me...

This project took me 1 hour and 30 minutes

---

## Connecting to an EC2 Instance

Connectivity means how different parts of my network talk to each other. Connectivity is important because this is how data flows smoothly from one resource to another. How data is delivered without delay and securely.

My first connectivity test was whether I could connect to my Public Instance using EC2 instance connect.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is used to accessed my public server directly using AWS Management Console, SSH is still used but private keys are directly managed.

My first attempt at getting direct access to my public server resulted in an error, because my public security group only allowed inbound HTTP traffic to access my EC2 instance and SSH traffic is not allowed.

I fixed this error by adding an inbound rule to my Public Server Security Group that allows any IPv4 traffic can access the EC2 intances using SSH on port 22. 

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is is used to check if there is a connection between two components in a network e.g., Public Server and Private Server. I used ping to test the connectivity between my Public Server and Private Server.

The ping command I ran was "Ping followed by the Private Server's IPv4 address" where it sends a message to a IPv4 address and checks if it have establish a conection to a host, by receiving a reply from that IPv4 address we can confirm that a connection is establish between two servers.

The first ping returned NO reply. This meant the two EC2 instance are not connected to each other or the private server was blocking inbound or outbound ICMP traffic.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by checking the route table if the IPv4 CIDR block is correct, then the route tables if it is directed to the correct destination, then the Network ACLs if ICMP is allowed inbound and outbound in that IP range, lastly is the Public Security Group inbound rules is allowed to receive a reply from the the Private Securtiy group.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is is used to test connectivity in a network. We can test connectivity by using curl to upload or retrieve a data from a server or we can also use to transfer data to or from a server.

I used curl to test the connectivity between my public server and the public internet.

### Ping vs Curl

Ping and curl are different because ping test a connectivity by sending a message to the server's IPv4 Address while Curl is used to transfer data to and from a server or retrieve data from a server. Curl is followed by a website address.

---

## Connectivity to the Internet

I ran the curl command "curl https://nextwork.ai/projects/aws-networks-connectivity", which returned the HTML data of this website address from a public server.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-networks-connectivity_8ee57662)

---

---
