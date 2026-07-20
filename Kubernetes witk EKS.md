<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launch a Kubernetes Cluster

**Project Link:** [View Project](http://nextwork.ai/projects/aws-compute-eks1)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## Launch a Kubernetes Cluster

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_e5f6g7h8)

---

## Introducing Today's Project!

In this project, I will launch and connect a EC2 instances, create my own Kubernetes clusters, monitor cluster creation with CloudFormation, and access the cluster using IAM cluster entry. 

### What is Amazon EKS?

### One thing I didn't expect

### This project took me...

---

## What is Kubernetes?

Kubernetes is an orchestration platform that manages all your containers in all servers, it scales them automatically and make sure it runs where they should. Companies and developers use Kubernetes because it automatically manages containers in which developers can focus more on building apps rather than manually managing containers.

I used eksctl to create a EKS clusters in the command line. The create cluster command I ran defined the name of the cluster, the node group name, node-type, nodes to use when scaling, cluster version, and the specific Region where it is launched.

I initially ran into two errors while using eksctl. The first one was because eksctl is not installed in my EC2 working environment. The second one was because EC2 does not have a role to create an EKS cluster.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_ff9bfc221)

---

## eksctl and CloudFormation

CloudFormation helped create my EKS cluster because eksctl uses CloudFormation in creating the clusters when I run eksctl create command. It created VPC resources because it is used by containers to connect with each other and the internet privately. Eksctl creates a new VPC.

There was also a second CloudFormation stack for nodes. Nodes are servers that run your containers. The difference between a cluster and node group is cluster is the environment that Kubernetes manages for the app containers while node groups are their servers the runs the containers, for easy management we can group nodes to easily control based on their resource limits and instance types.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_w3e4r5t6)

---

## The EKS console

I had to create an IAM access entry in order to view my nodes. An access entry is handshake between AWS and Kubernetes, the entry maps your IAM role to a RBAC which the cluster will let you access your nodes. I set it up using the Access Entry page within the EKS management console.

It took atleast 35 minutes to create my cluster. Since I'll create this cluster again in the next project of this series, maybe this process could be sped up if I used the CloudFormation template (events and resources) that is saved when I created my first EKS cluster.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_e5f6g7h8)

---

## EXTRA: Deleting nodes

Did you know you can find your EKS cluster's nodes in Amazon EC2? This is because the EC2 is the node in Kubernetes clusters/setups using AWS.

Desired size means the number of nodes you want running in your node group. Mininum and maximum sizes are helpful because it automatically adjust resources based from the desired size in high demand-period of your application.

When I deleted my EC2 instances Kubernetes clusters automatically creates new EC2 instances. This is because Kubernetes clusters need new nodes to keep the apps running on its desired states, this is one of the benefits of Kubernetes it makes sure that apps are running even when some nodes fail.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_q7r8s9t0)

---

---
