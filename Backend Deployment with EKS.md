<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploying a Backend Application on Amazon EKS

**Author:** RonJedrick
**Contact:** jedrickron3@gmail.com
 
**Project Series:**

- [Launch a Kubernetes Cluster](http://nextwork.ai/projects/aws-compute-eks1)
- [Set Up Kubernetes Deployment](http://nextwork.ai/projects/aws-compute-eks2)
- [Create Kubernetes Manifests](http://nextwork.ai/projects/aws-compute-eks3)
- [Deploy Backend with Kubernetes](http://nextwork.ai/projects/aws-compute-eks4)

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_e5f6g7h8" alt="Launching a Kubernetes cluster on Amazon EKS" width="700" />

---

## Overview

This project documents the end-to-end process of deploying a containerized backend application on **Amazon EKS (Elastic Kubernetes Service)**. It covers everything from launching a Kubernetes cluster on AWS, containerizing a backend application, writing Kubernetes manifests, deploying the application, and verifying the deployment through the EKS console.

The work was completed across four stages:

1. **Launching a Kubernetes cluster** using `eksctl` and EC2
2. **Preparing the deployment** by containerizing the backend and pushing the image to Amazon ECR
3. **Writing Kubernetes manifests** (Deployment and Service) to define how the app runs and how it's exposed
4. **Deploying and verifying** the application using `kubectl` and the EKS console

---

## Tools & Technologies

- **Amazon EKS** – managed Kubernetes service used to run the application
- **eksctl** – CLI tool used to create and delete the EKS cluster
- **kubectl** – CLI tool used to manage and debug the cluster and apply manifests
- **Amazon ECR** – container registry used to store the backend's container image
- **Docker** – used to build the container image
- **Amazon EC2** – hosted the working environment and, later, the cluster's worker nodes
- **AWS CloudFormation** – provisioned behind the scenes by `eksctl` to create the cluster's VPC and node group
- **Git** – used to clone the backend application source code
- **IAM** – used to grant cluster access via Access Entries

---

## What is Kubernetes?

Kubernetes is an orchestration platform that manages containers across a fleet of servers. It automatically scales containers and keeps them running in their desired state, which lets developers focus on building applications instead of manually managing infrastructure.

**Amazon EKS** is AWS's managed Kubernetes service — it handles the heavy lifting of running the Kubernetes control plane so you can focus on deploying workloads.

---

## Step 1: Launching a Kubernetes Cluster

I connected to an EC2 instance and used `eksctl` from the command line to create an EKS cluster. The `create cluster` command specified the cluster name, node group name, node type, scaling limits, Kubernetes version, and AWS Region.

**Cluster vs. Node Group:**

- A **cluster** is the environment Kubernetes manages for application containers.
- A **node group** is a set of servers (nodes) that actually run the containers, grouped together for easier management based on resource limits and instance types.

Under the hood, `eksctl` uses **AWS CloudFormation** to provision the cluster. This included one CloudFormation stack to create the VPC (which lets containers communicate with each other and the internet privately), and a second stack to create the node group.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_ff9bfc221" alt="Creating an EKS cluster with eksctl" width="600" />

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_w3e4r5t6" alt="CloudFormation stacks created by eksctl" width="600" />

To view the cluster's nodes in the EKS console, I created an **IAM Access Entry** — essentially a handshake between AWS and Kubernetes that maps an IAM role to Kubernetes RBAC, granting console access to the cluster.

**Troubleshooting:**

- `eksctl` wasn't initially installed in the EC2 environment — installed it manually.
- EC2 didn't have the IAM role/permissions needed to create an EKS cluster — resolved by attaching the correct role.

**Bonus finding:** EKS nodes are actually just EC2 instances under the hood. Deleting an EC2 instance that's part of a node group causes Kubernetes to automatically spin up a replacement, since the cluster works to maintain its desired state — a core benefit of Kubernetes' self-healing design.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks1_q7r8s9t0" alt="EKS node group backed by EC2 instances" width="600" />

⏱️ Took approximately 35 minutes.

---

## Step 2: Preparing the Backend for Deployment

### Retrieving the backend

I cloned the backend application from GitHub. The backend is the "brain" of the application — it processes user requests and handles saving/retrieving data server-side. This particular backend accepts a search request, fetches and processes the relevant data, then returns it as a JSON response.

**Key backend files:**

- **`requirements.txt`** – lists the dependencies every container needs installed
- **`Dockerfile`** – instructs Docker on how to build the backend image (e.g. `FROM python:3.9-alpine`, `LABEL Author="NextWork"`, `COPY requirements.txt requirements.txt`, `WORKDIR /app`)
- **`app.py`** – the main backend logic: app setup, routing, data fetching, and sending responses

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_1ebb86c71" alt="Cloning the backend application code" width="600" />

### Building the container image

Kubernetes requires a container image to deploy an application. Using Docker to build this image means the app will run consistently across different environments, since every container built from the image is identical.

**Troubleshooting:** Building the Docker image initially failed with a permissions error because I was logged in as the `ec2-user`, while Docker was installed under the root account. I fixed this by adding the `ec2-user` to the `docker` group, which grants permission to run Docker commands without root access.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_45e6c3de5" alt="Building the backend Docker container image" width="600" />

### Storing the image in Amazon ECR

I pushed the built image to **Amazon ECR**, AWS's container registry. Using ECR alongside EKS — both within AWS — simplified authentication and made it easy for EKS to pull the image with minimal setup. Container registries ensure that every environment pulling the image gets identical files, libraries, and settings.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_l2m3n4o5" alt="Storing the container image in Amazon ECR" width="600" />

⏱️ Took approximately 1 hour 30 minutes.

---

## Step 3: Writing Kubernetes Manifests

Kubernetes manifests are instruction sets that tell Kubernetes how to run an application — essentially a manual for how to set up and manage the app.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_b01876554" alt="Kubernetes Deployment manifest" width="600" />

### Deployment Manifest

The Deployment manifest tells Kubernetes which container image to deploy and how many copies (replicas) of it to run. I annotated my manifest line by line to understand each field, which will make it faster to edit or write new manifests in the future.

A key setting is **`replicas`** — the number of identical Pod copies to run. Setting this to `3` means Kubernetes maintains 3 running Pods of the backend at all times.

**Pods vs. Containers:** A Pod is the smallest deployable unit in Kubernetes. It wraps one or more containers together so they share the same network space and storage, allowing them to communicate and share data seamlessly.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_6aae73e71" alt="Annotated Kubernetes Deployment manifest with replicas defined" width="600" />

### Service Manifest

While the Deployment manifest creates and manages the application's Pods, it doesn't expose them to the outside world — that's the job of the **Service manifest**. It defines which port is opened on each node in the cluster and how external traffic gets routed to the running Pods.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_b01876555" alt="Kubernetes Service manifest" width="600" />

⏱️ Took approximately 45 minutes.

---

## Step 4: Deploying and Verifying the Backend

### Deploying with kubectl

With both manifests written, I deployed the backend by applying the Deployment and Service manifests using `kubectl`.

**kubectl vs. eksctl:** These two tools serve different purposes — `eksctl` is used to create and delete the EKS cluster itself, while `kubectl` is used to manage workloads _within_ the cluster, such as applying manifests and debugging.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks4_6cfb382f2" alt="Applying manifests with kubectl to deploy the backend" width="600" />

### Verifying the deployment

As an extension, I used the **EKS console** to verify the deployment and monitor the running nodes. This required setting up an IAM Access Entry granting my logged-in user Administrator access within the cluster.

Once inside, I could see the Pods running across each node, along with per-Pod events describing what happened during deployment — confirming the backend deployed successfully.

<img src="http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks4_3b391f873" alt="Verifying Pods and deployment events in the EKS console" width="600" />

⏱️ Took approximately 45 minutes.

---

## Key Takeaways

- **EKS clusters** are built on top of EC2 and CloudFormation, and `eksctl` abstracts away most of the manual provisioning.
- **Container images** (built with Docker, stored in ECR) are what make Kubernetes deployments portable and consistent across environments.
- **Manifests** are declarative instructions — the Deployment manifest defines _what_ to run, and the Service manifest defines _how it's reached_.
- **Pods** are the fundamental unit Kubernetes schedules, and can contain one or more tightly coupled containers.
- **IAM Access Entries** bridge AWS IAM and Kubernetes RBAC, controlling who can view and manage cluster resources via the console.
- Kubernetes' self-healing behavior (e.g., replacing a deleted node automatically) is one of its biggest advantages for maintaining application uptime.

---

## What's Next

Areas I'd like to explore further:

- The deeper distinction between containers and Pods, and when to run multiple containers in a single Pod
- Speeding up cluster creation by reusing the saved CloudFormation template from the first cluster build
- Exploring Horizontal Pod Autoscaling and how it interacts with node group min/max sizing
