# 🐳 Docker Lab 3: Private Registry, WordPress, and Reverse Proxy     (Nginx)

This project shows how to use Docker and Docker Compose. We will make a local registry, run a WordPress site, and use Nginx to route traffic to a Flask app.

## Part 1: Local Insecure Docker Registry

First, we need to start a local registry to store our custom images.

**Command to run the registry:**

```bash
docker run -d -p 5000:5000 --name registry registry:3
```

![first command](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Running%20docker%20registry.png)

Next, we tell Docker to trust this local insecure registry. We edit the daemon.json file.

![Adding registry](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Addind%20insceure%20registries.png)

Now, we create a custom Nginx image. We use Alpine as the base image. Here is the Dockerfile.

![Dockerfile](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Docker%20file.png)

Command to build the image:
```bash
docker build -t nginx-image .
```

![Building first image](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Building%20the%20first%20image.png)


After building the image, we must tag it with our local registry address.

Command to tag the image:

```bash
docker tag my-nginx localhost:5000/nginx-image
```
Finally, we push the image to our local registry.

Command to push the image:
```bash
docker push localhost:5000/nginx-image
```

![Pushing the image](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/The%20images%20has%20pushed%20successfully.png)

---

## Part 2: WordPress and MySQL
In this part, we use Docker Compose to run WordPress and a MySQL database together. We map the database to a local folder and open port 8082 for WordPress.

Here is the docker-compose.yml file.

![first yaml file](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Docker%20compose%20file.png)

Command to start the services:

![Compose up](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Docker%20compose%20up.png)
```bash
docker compose up -d
```

Now we can open the browser and see the WordPress setup page.

![Verifying wordpress](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Verify%20wordpress.png)

---

## Part 3: Flask App with Nginx Reverse Proxy
In the last part, we run a Flask app and put Nginx in front of it to act as a reverse proxy.

First, we push our Flask app image to the private registry.

![Pushing flask to private](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Pushing%20flask%20img%20to%20private%20register.png)

We need an nginx.conf file. This file tells Nginx to send traffic from port 80 to the Flask app on port 5000.

![nginx conf](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Config%20file%20for%20nginx%20to%20forward%20traffic%20to%20flask.png)

We create a new docker-compose.yml file. It will pull the Flask image from our private registry and start the Nginx proxy.

![second yaml file](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Compose%20file%20for%20nginx%20and%20flask.png)

Here, Docker Compose is pulling the image from our local registry.
```bash
docker compose up -d
```

We start the containers. Everything works fine.

We test the link in the browser, and the Flask app opens successfully through Nginx.

![last image](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab3/Screenshots/Last%20image.png)
