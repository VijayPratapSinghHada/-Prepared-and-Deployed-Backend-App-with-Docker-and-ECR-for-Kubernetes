<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Kubernetes Deployment

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks2)

**Author:** Vijay Pratap Singh Hada  
**Email:** vijaypratapsinghhada9@gmail.com

---

## Set Up Kubernetes Deployment

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks2_45e6c3de5)

---

## Introducing Today's Project!

In this project, I'll get an app's backend ready for deployment using Kubernetes. This is part two of a four-part series on Kubernetes with AWS. I'll download a backend application from GitHub, create a Docker image, upload it to an Amazon ECR repository, and fix any installation issues that may come up.

### Tools and concepts

I used Amazon EKS, Git, and Docker to set up and manage the backend application for deployment. Key steps include launching an EC2 instance, cloning the backend code from GitHub, building a Docker image, pushing the image to Amazon ECR, and creating an API to fetch data from the Hacker News Search API. 

### Project reflection

This project took me approximately 90 minutes to complete. The most challenging part was troubleshooting permissions and installation errors. My favorite part was building the Docker image and pushing it to Amazon ECR, as it made everything feel more real and functional.

Something new that I learned from this experience was how to integrate a backend application with external APIs using Flask.

---

## What I'm deploying

To set up today's project, I launched a Kubernetes cluster. Steps I took included launching an EC2 instance, selecting the Amazon Linux 2023 AMI, and choosing the t2.micro instance type. I connected to the EC2 instance using EC2 Instance Connect and installed eksctl, a tool for managing EKS clusters. Then, I created an IAM role for my EC2 instance to grant it permissions, followed by attaching this role to the instance. Finally, I ran a command to create the EKS cluster, setting its name and specifications.

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend means it's responsible for processing user requests and managing data on the server side. I got the backend code by cloning the repository from GitHub, which gives me a complete copy of the code needed to run my application. After installing Git on the EC2 instance, I used the command to clone the repository, and now I have all the necessary files to work with.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks2_1ebb86c71)

---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because the container image packages the application and all its dependencies, allowing it to run smoothly in different environments. By using the Dockerfile written by my team member, I can create an image that Kubernetes will use to deploy multiple identical containers.

When I tried to build a Docker image of the backend, I ran into a permissions error because the ec2-user, which I was logged in as, didn't have the necessary rights to run Docker commands. When Docker was installed, it was set up for the root user, meaning only the root user could run Docker commands without additional permissions. Although I could use "sudo" to run commands with elevated rights, it's better practice to give the ec2-user the permissions needed for Docker. This way, I can build and manage container images without having to use "sudo" every time.

To solve the permissions error, I added the ec2-user to the Docker group. The Docker group allows users to run Docker commands without needing root privileges. By using the command sudo usermod -a -G docker ec2-user, I ensured that ec2-user can now execute Docker commands smoothly without having to use "sudo" each time. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks2_45e6c3de5)

---

## Container Registry

I'm using Amazon ECR in this project to store and manage my container images securely. ECR is a good choice for the job because it is an AWS service that integrates easily with Elastic Kubernetes Service (EKS), allowing for smooth deployment of my container images with minimal authentication setup.

Container registries like Amazon ECR are great for Kubernetes deployment because they store container images in a central location that Kubernetes can easily access. This setup allows Kubernetes to pull the latest image on demand, ensuring consistent application behavior across all nodes in the cluster. If we didn't use a container registry, we would need to manually preload and update each node with the image, which would be time-consuming and prone to errors.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks2_l2m3n4o5)

---

## EXTRA: Backend Explained

After reviewing the app's backend code, I've learned that the backend fetches data based on a search topic provided by the user. The code uses Flask to create an API that connects with the Hacker News Search API, processes the data, and returns it as formatted JSON. This allows users to easily access relevant information based on their search queries, enabling smooth communication between the backend and the external API.

### Unpacking three key backend files

The requirements.txt file lists the necessary dependencies for the backend application to run properly. It includes specific packages that the app needs, such as Flask for creating web applications, Flask-RESTx for building APIs, Requests for retrieving data from sources like the Hacker News API, and Werkzeug for routing requests within the app.

The Dockerfile gives Docker instructions on how to build a container image for the backend application. Key commands in this Dockerfile include setting the base environment with Python, copying the application code, installing necessary dependencies from requirements.txt, and specifying the command to run the app. 

The app.py file contains the main code for the backend application. It sets up the Flask framework and defines a route that users can access to perform searches. When a user visits the URL, the app fetches data from the Hacker News Search API based on the topic provided. It retrieves important details like the ID, title, and URL of the content, then formats this information as JSON to send back to the user.

---

---
