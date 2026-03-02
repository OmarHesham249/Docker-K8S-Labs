# Docker Lab 2

This repository contains the solution for Lab 2 of the Docker course at the Information Technology Institute (ITI). The lab is divided into two parts: building a Python Flask application and configuring an Nginx web server with specific networking and storage requirements.

---

## 🚀 Part 1: Python Flask Image

### Objective
* Build a Python Flask image based on `alpine` or `ubuntu`.
* Set a memory limit of **100MB**.
* Publish port `5000` on the container to port `80` on the host.
* Push the image to Docker Hub.

### 1. The Dockerfile
I created a Dockerfile to containerize the basic flask application.

![Dockerfile Screenshot](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Docker%20file.png)
### 2. Building the Image
Building the image locally using `docker build`.

![Building Image](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Testing%20building%20Image%20locally.png)

### 3. Running the Container & Port Mapping
Running the container with the required memory limit and port mapping (`-m 100m -p 80:5000`).

![Running container](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Running%20the%20container.png)

```bash
docker run -d -m 100m -p 80:5000 --name flask-app iti-flask-lab2
```

![Testing portmapping](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Testing%20container%20%26%26%20port%20mapping.png)

### 4. Pushing to Docker Hub
Successfully pushed the tagged image to my Docker Hub account.

![Pushing to docker hub](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Pushing%20the%20image%20to%20docker%20hub.png)

https://hub.docker.com/repository/docker/omarhesham249/omar-flask-img/

---

## 🌐 Part 2: Nginx Web Server & Networking
Objective
Create a custom bridge network named iti-network with subnet 10.0.0.0/8.

Run an Nginx container named webserver-iti.

Configure Nginx to listen on port 8080 inside the container.

Use Volume Mounting to serve a custom index.html page.

### 1. Creating the Network
Created a bridge network with the specific subnet.

![Creating network](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Creating%20iti%20network.png)

```bash
docker network create --driver bridge --subnet 10.0.0.0/8 iti-network
```
### 2. Custom Index Page (Volume Mounting)
I prepared an index.html file containing the required text: <h1>Lab 2 ITI - Omar Hesham</h1>. This file is mounted to the container to replace the default Nginx page.

```bash
echo "<h1>Lab 2 ITI - Omar Hesham</h1>" > index.html
docker run -v $(pwd)/Data:/usr/share/nginx/html
```

4. Running the Nginx Container
Executed the container on the iti-network, mapping port 8080 to 8080, and handling the read-only volume mount (using :Z for SELinux context).

![Run container](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Creating%20the%20container%20for%20task%202.png)

```bash
docker run -d --name webserver-iti \
  --network iti-network \
  -p 8080:8080 \
  -v $(pwd)/index.html:/usr/share/nginx/html/index.html:ro,Z \
  nginx:alpine
```
4. Verification

Verifying the setup by accessing the web server.

![Verify](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab2/Screenshots/Adding%20content%20using%20volume%20mounting.png)
