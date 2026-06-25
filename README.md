
# Docker Static Website Hosting using Nginx

## Project Overview

This project demonstrates how to host a static website using Docker and Nginx. The website is containerized using Docker and served through an Nginx web server running inside a container.

The project covers:

* Dockerfile creation
* Docker image building
* Container deployment
* Port mapping
* Docker volumes
* Docker networking
* AWS EC2 deployment
* Basic container monitoring

---

## Architecture

```text
Developer
    |
    v
Static Website Files
    |
    v
Docker Build
    |
    v
Docker Image
    |
    v
Docker Container
    |
    v
Nginx Web Server
    |
    v
Browser
```

---

## Project Structure

```text
docker-static-website-nginx/
│
├── website/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── Dockerfile
├── docker-compose.yml
├── README.md
├── notes.md
├── architecture.md
├── troubleshooting.md
└── interview-questions.md
```

---

## Technologies Used

* Docker
* Nginx
* HTML
* CSS
* JavaScript
* Ubuntu Linux
* AWS EC2

---

## Dockerfile

```dockerfile
FROM nginx:latest

COPY website/ /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

---

## Build Docker Image

```bash
docker build -t static-website .
```

Verify image:

```bash
docker images
```

---

## Run Docker Container

```bash
docker run -d \
--name static-website \
-p 8080:80 \
static-website
```

Verify:

```bash
docker ps
```

---

## Access Website

Local Machine:

```text
http://localhost:8080
```

AWS EC2:

```text
http://<EC2-Public-IP>
```

---

## Docker Compose

```yaml
version: '3'

services:
  website:
    image: static-website
    container_name: static-website
    ports:
      - "8080:80"
```

Run:

```bash
docker compose up -d
```

---

## Volume Mounting

```bash
docker run -d \
-p 8080:80 \
-v $(pwd)/website:/usr/share/nginx/html \
nginx
```

Benefits:

* Live code updates
* Faster development
* No image rebuild

---

## Custom Docker Network

Create network:

```bash
docker network create devops-network
```

Run container:

```bash
docker run -d \
--network devops-network \
--name static-website \
-p 8080:80 \
static-website
```

---

## Deployment on AWS EC2

### Install Docker

```bash
sudo apt update

sudo apt install docker.io -y

sudo systemctl start docker

sudo systemctl enable docker
```

### Build Image

```bash
docker build -t static-website .
```

### Run Container

```bash
docker run -d \
--name static-website \
-p 80:80 \
static-website
```

### Security Group

Allow:

* SSH (22)
* HTTP (80)

---

## Monitoring

Monitor containers using cAdvisor.

```bash
docker run -d \
--name cadvisor \
-p 8081:8080 \
-v /:/rootfs:ro \
-v /var/run:/var/run:ro \
-v /sys:/sys:ro \
-v /var/lib/docker:/var/lib/docker:ro \
gcr.io/cadvisor/cadvisor
```

Access:

```text
http://localhost:8081
```

---

## Key Docker Commands

```bash
docker images

docker ps

docker ps -a

docker logs static-website

docker stop static-website

docker start static-website

docker restart static-website

docker rm static-website
```

---

## Project Outcomes

* Learned Docker fundamentals
* Created custom Docker images
* Deployed Nginx containers
* Implemented port mapping
* Used Docker volumes
* Configured Docker networking
* Deployed application on AWS EC2
* Practiced container troubleshooting

---

## Author

Swapnil Girme

DevOps Engineer | Docker | Kubernetes | Jenkins | AWS | Terraform | Linux
