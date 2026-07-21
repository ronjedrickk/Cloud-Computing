<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Kubernetes Deployment

**Project Link:** [View Project](http://nextwork.ai/projects/aws-compute-eks2)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## Set Up Kubernetes Deployment

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_45e6c3de5)

---

## Introducing Today's Project!

In this project, I will launch a launch and EC2 instance and create Kubernetes cluster using Amazon EKS. Prepare Kubernetes deployment using Amazon ECS because this deployment requires apps to be containerized and for there to be a container image.

### Tools and concepts

I used Amazon EKS, Git, EC2 instance, Amazon ECR, Docker, and eksctl to prepare the deployment of an application. Key steps include accessing the EC2 instance to create a Kubernetes cluster, creating a container image, and storing the container image to Amazon ECR.

### Project reflection

This project took me approximately one hour and thirty minutes to finish and The most challenging part was navigating the command line, and this is also my favourite part.

Something new that I learnt from this experience was it is easier to deploy an app using container images especially when the services used are in one environment e.g., Amazon EKS and Amazon ECR both in AWS Cloud.

---

## What I'm deploying

To set up today's project, I launched a Kubernetes cluster. Steps I took to do this included connect to my EC2 instance using EC2 Instance Connect. Downloaded eksctl in my EC2 instance, a command line tool used to create Kubernetes clusters using commands.

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend means it's the brain of the application. This is where the app processed user request and save and retrieved data. It works in the background server side. I retrieved backend code by cloning it from ma GitHub repository.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_1ebb86c71)

---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because Kubernetes needs container image for successful app deployment and container images let's Docker create more identical containers so that my application can run consistently across different environments.

When I tried to build a Docker image of the backend, I ran into a permissions error because I am currently logged in as EC2 user. Since Docker is installed in the root account.  So only the root user level can interact with the Docker engine.

To solve the permissions error, I added the EC2 user to the docker group.  The Docker group is a group in the Linux system that grants user permissions to run Docker commands.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_45e6c3de5)

---

## Container Registry

I'm using Amazon ECR in this project to store my container images. ECR is a good choice for the job because it let's EKS to deploy container images with minimal authentication.

Container registries like Amazon ECR are great for Kubernetes deployment because users can pull the container images and all the files, libraries and settings of the application are the same even on different environments.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks2_l2m3n4o5)

---

## EXTRA: Backend Explained

After reviewing the app's backend code, I've learnt that how it works from the background from sending a request based on search topic, the API fetches the data and process it then sending the data back in JSON format.

### Unpacking three key backend files

The requirements.txt file lists all the dependencies and libraries that every container needs to install when it gets created.

The Docker file gives Docker instructions and defines how the backend should be built. It installs the necessary dependencies, files and set up commands a container needs to start and run the application. Key commands in this Docker file include the environment the app is using (FROM python:3.9-alpine), the author (LABEL Author="NextWork"), (COPY requirements.txt requirements.txt), and the working directory (WORKDIR /app)

The app.py file contains the main code of the backend. Its functions are setting up the app and routing, fetching data, and sending the response.

---

---
