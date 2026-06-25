
# Docker Project 1: Static Website Hosting using Docker & Nginx

## Project Overview

This project demonstrates how to containerize and deploy a static website using Docker and Nginx. The website consists of HTML, CSS, and JavaScript files served through an Nginx web server running inside a Docker container.

The objective of this project is to understand Docker image creation, container deployment, port mapping, volume mounting, networking, and basic monitoring concepts.

---

# Problem Statement

Traditionally, hosting a website requires installing and configuring a web server manually on each machine. Different environments often lead to inconsistencies and deployment issues.

Docker solves this problem by packaging the application and its dependencies into a portable container that can run consistently across development, testing, and production environments.

---

# Project Architecture

Developer
→ Creates Website Files

Website Files
→ Docker Build

Docker Image
→ Docker Run

Docker Container
→ Nginx Web Server

Nginx
→ Serves Static Website

Browser
→ Accesses Website

---

# Project Structure

docker-static-website-nginx/

├── website/

│   ├── index.html

│   ├── style.css

│   └── script.js

├── Dockerfile

├── docker-compose.yml

├── notes.md

├── architecture.md

├── troubleshooting.md

├── interview-questions.md

└── README.md

---

# Technologies Used

* Docker
* Nginx
* HTML
* CSS
* JavaScript
* Ubuntu Linux
* AWS EC2

---

# Website Files

## index.html

Main webpage displayed to users.

Responsibilities:

* Defines page structure
* Loads CSS and JavaScript
* Displays website content

## style.css

Provides styling for:

* Colors
* Layout
* Fonts
* Responsive appearance

## script.js

Provides client-side functionality.

Example:

* Button click actions
* Alerts
* Dynamic webpage interactions

---

# Dockerfile Explanation

FROM nginx:latest

COPY website/ /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

## Explanation

### FROM nginx:latest

Downloads the official Nginx image from Docker Hub.

### COPY website/ /usr/share/nginx/html/

Copies website files into Nginx's default web root directory.

### EXPOSE 80

Documents that the application listens on port 80.

### CMD

Starts Nginx in the foreground mode.

Without this command, the container would stop immediately.

---

# Building Docker Image

Command:

docker build -t static-website .

Explanation:

* docker build creates image
* -t assigns image name
* . indicates current directory contains Dockerfile

Verify:

docker images

---

# Running Docker Container

Command:

docker run -d --name static-website -p 8080:80 static-website

Explanation:

* -d runs container in background
* --name assigns container name
* -p maps host port to container port

Port Mapping:

Host Port 8080
↓

Container Port 80

Access Website:

http://localhost:8080

or

http://EC2-Public-IP

---

# Container Lifecycle

Create Image
↓

Run Container
↓

Container Running
↓

Stop Container
↓

Restart Container
↓

Remove Container

Commands:

docker stop static-website

docker start static-website

docker restart static-website

docker rm static-website

---

# Docker Volume Concept

Without Volume:

Changes require rebuilding image.

With Volume:

docker run -d 
-p 8080:80 
-v $(pwd)/website:/usr/share/nginx/html 
nginx

Benefits:

* Live code updates
* Faster development
* No image rebuild required

---

# Docker Networking

Create custom network:

docker network create devops-network

Run container:

docker run -d 
--network devops-network 
--name static-website 
-p 8080:80 
static-website

Benefits:

* Container communication
* Isolation
* Better security

---

# Monitoring with cAdvisor

Purpose:

Monitor Docker containers.

Metrics:

* CPU Usage
* Memory Usage
* Network Usage
* Disk Usage

Run:

docker run -d 
--name cadvisor 
-p 8081:8080 
-v /:/rootfs:ro 
-v /var/run:/var/run:ro 
-v /sys:/sys:ro 
-v /var/lib/docker:/var/lib/docker:ro 
gcr.io/cadvisor/cadvisor

Access:

http://localhost:8081

---

# Deployment on AWS EC2

Step 1

Launch Ubuntu EC2 Instance.

Step 2

Install Docker.

sudo apt update

sudo apt install docker.io -y

Step 3

Start Docker Service.

sudo systemctl start docker

sudo systemctl enable docker

Step 4

Build Image.

docker build -t static-website .

Step 5

Run Container.

docker run -d 
--name static-website 
-p 80:80 
static-website

Step 6

Open Security Group.

Allow:

* SSH 22
* HTTP 80

Step 7

Access:

http://Public-IP

---

# Common Issues

## Docker Permission Denied

Error:

permission denied while trying to connect to docker.sock

Solution:

sudo usermod -aG docker $USER

newgrp docker

---

## Dockerfile Not Found

Error:

no such file or directory Dockerfile

Solution:

Ensure Dockerfile exists in current directory.

Verify:

ls -la

---

## Port Already Allocated

Error:

Bind for 0.0.0.0:80 failed

Solution:

Find running container:

docker ps

Stop conflicting container.

---

# Real-World Use Cases

* Portfolio Websites
* Landing Pages
* Company Documentation Sites
* Product Information Pages
* Internal Dashboards
* Static Frontend Applications

---

# Key Learnings

* Docker Image Creation
* Docker Containers
* Dockerfile Concepts
* Nginx Basics
* Port Mapping
* Volumes
* Networking
* Monitoring
* AWS EC2 Deployment
* Container Troubleshooting

---

# Resume Description

Built and deployed a static website using Docker and Nginx. Created custom Docker images using Dockerfile, implemented volume mounting for live updates, configured container networking, monitored containers using cAdvisor, and deployed the application on AWS EC2 with Docker-based hosting.
