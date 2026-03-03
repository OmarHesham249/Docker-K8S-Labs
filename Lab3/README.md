# 🐳 Docker & Docker Compose Lab: Private Registry, WordPress, and Reverse Proxy

## 📝 Overview

This repository contains the documentation and implementation of Lab 3, focusing on advanced Docker concepts, including setting up a self-hosted private registry, building custom images, and orchestrating multi-container environments using Docker Compose.

The project is divided into three main parts:

---

## 📌 Part 1: Local Insecure Docker Registry & Custom Images

In this section, a private Docker registry was established, and a custom Nginx image was built and pushed to it.

**Key Steps Performed:**

- Deployed a local insecure Docker registry (`registry:2`) on port `5000`.
- Configured the Docker daemon to trust the insecure registry (`Addind insecure registries.png`).
- Created a custom `Dockerfile` based on `alpine:latest` to install and run Nginx (`Docker file.png`, `Building the first image.png`).
- Tagged the generated image and successfully pushed it to the local private registry (`Tagging and error with pushing.png`, `The images has pushed successfully.png`).

---

## 📌 Part 2: Multi-Container Deployment (WordPress & MySQL)

This section demonstrates orchestrating a multi-container environment using Docker Compose.

**Key Steps Performed:**

- Wrote a `docker-compose.yml` file to deploy WordPress and MySQL (`Docker compose file.png`).
- Configured environment variables to establish the database connection.
- Implemented a **Bind Mount** to persist MySQL data securely on the host machine at `/var/lib/mysql`.
- Exposed the WordPress application on host port `8080`.
- Successfully started the services and verified the WordPress installation page (`Verify wordpress.png`, `Docker compose up.png`).

---

## 📌 Part 3: Flask App with Nginx Reverse Proxy

The final part integrates the private registry with Docker Compose and implements a reverse proxy architecture.

**Key Steps Performed:**

- Tagged and pushed a custom Flask application image to the local private registry (`Pushing flask img to private register.png`).
- Created an `nginx.conf` file to act as a reverse proxy, forwarding traffic from port 80 to the internal Flask container on port 5000 (`Config file for nginx to forward traffic to flask.png`).
- Developed a `docker-compose.yml` file with two services:
  1.  **Flask App:** Pulled dynamically from the local private registry (`192.168.241.138:5000/my-flask-app:latest`).
  2.  **Nginx Proxy:** Configured to map the custom `nginx.conf` file using volumes (`Compose file for nginx and flask.png`).
- Successfully verified the proxy routing and the Flask app's functionality (`Last image.png`, `verifying it works.png`).

---

## 📂 Repository Structure References

_(Note: Screenshots documenting each step are included in the repository for verification)._

- Registry Setup: `Running docker registry.png`
- Docker Compose Pulling from Private: `docker compose pulling from private.png`
- Final Output: `Last image.png`
