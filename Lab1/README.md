# Docker Essentials Lab - ITI System Admin Track

This repository contains the solution for the Docker Lab assignment. The tasks cover Docker installation, container management, resource limiting (Cgroups), and demonstrating the OOM (Out Of Memory) Killer mechanism.

**Student Name:** Omar Hesham  
**Track:** ITI System Admin (Intake 46)  
**Environment:** Red Hat Enterprise Linux 9 (RHEL 9)

---

## 🚀 Task 1: Installation & Setup

### 1. Uninstalling Old Versions
Before installing Docker, I ensured a clean environment by removing any conflicting packages or old versions of Docker/Podman.

![Uninstall Old Versions](screenshots/image_44231d.png)

### 2. Installing Docker Engine
Successfully installed `docker-ce`, `docker-ce-cli`, and `containerd.io`.

![Installing Docker](screenshots/Installing%20Docker.jpg)

### 3. Starting & Testing Docker
Started the Docker service and verified the installation by running the `hello-world` container.

![Hello World Test](screenshots/Starting%20and%20Testing%20Docker%20with%20hello-world.jpg)

---

## 🐳 Task 2: Container Management (Nginx)

### 1. Pulling the Image
Pulled the `nginx:alpine` image from Docker Hub.

![Pull Nginx](screenshots/Pulling%20Nginx%20Image.jpg)

### 2. Running Nginx in Background
Ran the Nginx container in detached mode (`-d`) and assigned the specific name `Omar-ITI-46` as required.

```bash
docker run -d --name Omar-ITI-46 nginx:alpine
⚙️ Task 3: Resource Limits (Cgroups)
1. Limiting Memory & CPU
Created a container with strict resource limits:

Memory: 70MB

CPU: 1 Core

Bash
docker update --memory 70m --cpus 1.0 Omar-ITI-46
2. Verifying Cgroup Values
Navigated to the Cgroup v2 path to verify the configuration at the kernel level.

Memory Limit in Bytes: 73400320 (which equals 70MB).

CPU Quota: 100000 (100% of a period, equating to 1 Core).

💀 Task 4: Bonus - The OOM Killer
In this task, I demonstrated how the Linux Kernel handles a container that exceeds its allowed memory usage (Out Of Memory).

Scenario:
Created a container named memory-eater.

Set a hard limit of 50MB RAM and disabled Swap (--memory-swap 50m).

Executed a command to consume more than 50MB of RAM immediately.

Result:
The container was immediately killed by the system.

Status: Exited (137)

Exit Code 137: Indicates SIGKILL (9) + 128, confirming the OOM Killer action.
