<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create Kubernetes Manifests

**Project Link:** [View Project](http://nextwork.ai/projects/aws-compute-eks3)

**Author:** RonJedrick  
**Email:** jedrickron3@gmail.com

---

## Create Kubernetes Manifests

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_b01876555)

---

## Introducing Today's Project!

In this project, I will set up a Kubernetes manifest that tells how Kubernetes will deploy the application. Create a service manifest so that users can access my app.

### Tools and concepts

I used Amazon EKS, eksctl, Git, Docker, ECR, and EC2 instance to create a container images, store it in ECR, create a Kubernetes Manifest and Service manifest. Key concepts include using manifest as a manual that tells a system what to do.

### Project reflection

I chose to do this project today because I want to know how to create manifest and what are their uses.

It took me 45 minutes to set up my app for deployment and creating a service manifest.

---

## Project Set Up

### Kubernetes cluster

To set up today's project, I launched a Kubernetes cluster. Steps I took to do this included I used an eksctl command line tool in the EC2 instance server to create an Kubernetes clusters.

### Backend code

I retrieved the backend that I plan to deploy. An app's backend means it's the brain of the application. This is where the app processed user request and save and retrieved data. It works in the background server side. I retrieved backend code by cloning it from ma GitHub repository.

### Container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because Kubernetes needs container image for successful app deployment and container images let's Docker create more identical containers so that my application can run consistently across different environments.

Container registries like Amazon ECR are great for Kubernetes deployment because users can pull the container images and all the files, libraries and settings of the application are the same even on different environments.

---

## Manifest files

Kubernetes manifests are sets of instructions that tells how to run the application. Manifests are helpful because it serves as manual that tells a system how to set up and manage an app. 

A Kubernetes deployment manages multiple copies of the same containerized backend. The container image URL in my Deployment manifest tells Kubernetes the attributes of the container that we'd like Kubernetes to deploy.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_b01876554)

---

## Service Manifest

A Kubernetes Service exposes the application to external traffic. You need a Service manifest because the deployment manifest takes care in creating and managing the application and service manifest is used to expose the application to the outside world.

My Service manifest is compost of instructions on which port of the service is open on each node of the cluster. In which outside traffic are redirected.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_b01876555)

---

## Deployment Manifest

Annotating the Deployment manifest helped me understand and define the functions of each part of the deployment manifest because this will help me edit the deployment manifest faster or when I need to create new deployment manifest.

A notable line in the Deployment manifest is the number of replicas, which means these are the identical copies of our instances we'd like to deploy. Pods are relevant to this because they are the smallest deployable units in Kubernetes. 3 replicas means 3 pods.

One part of the Deployment manifest I still want to know more about is about containers and pods because I want to dig deeper into what are their differences.

![Image](http://nextwork.ai/hopeful_maroon_innocent_loquat/uploads/aws-compute-eks3_6aae73e71)

---

---
