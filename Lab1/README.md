# Docker Essentials Lab 1 - ITI System Admin

This repository contains the solution for the Docker Lab assignment. The tasks cover Docker installation, container management, resource limiting (Cgroups), and demonstrating the OOM (Out Of Memory) Killer mechanism.

**Student Name:** Omar Hesham  
**Track:** ITI System Admin (Intake 46)  
**Environment:** Red Hat Enterprise Linux 9 (RHEL 9)

---

## 🚀 Task 1: Installation & Setup

### 1. Uninstalling Old Versions
Before installing Docker, I ensured a clean environment by removing any conflicting packages or old versions of Docker/Podman.

### 2. Installing Docker Engine
Successfully installed `docker-ce`, `docker-ce-cli`, and `containerd.io`.

![Installing Docker](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab1/Screenshots/Installing%20Docker.png)

### 3. Starting & Testing Docker
Started the Docker service and verified the installation by running the `hello-world` container.

![Hello World Test](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab1/Screenshots/Starting%20and%20Testing%20Docker%20with%20hello-world.png)

---

## 🐳 Task 2: Container Management (Nginx)

### 1. Pulling the Image
Pulled the `nginx:alpine` image from Docker Hub.

![Pull Nginx](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab1/Screenshots/Pulling%20Nginx%20Image.png)

Then I checked for the Mmemory value that's having the default value which is MAX.

![Path of Container and memory value](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab1/Screenshots/Path%20of%20container%20cgroup%20and%20it's%20memory%20value.png)

### 2. Running Nginx in Background
Ran the Nginx container in detached mode (`-d`) and assigned the specific name `Omar-ITI-46` as required.

docker run -d --name Omar-ITI-46 nginx:alpine

## ⚙️ Task 3: Manual Resource Control (Cgroups v2)Instead of using Docker commands, 
###I navigated directly to the Cgroup v2 filesystem to inspect and manually enforce resource limits at the kernel level.
1. Locating the Cgroup PathIdentified the container's scope directory within /sys/fs/cgroup/system.slice/.
2. Applying Limits ManuallyI manually wrote the limit values into the controller files:

![Limiting](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab1/Screenshots/Limiting%20the%20memory%20to%2070M%20and%201%20core%20CPU.png)
   
Memory Limit (70MB): Calculated as $70 \times 1024 \times 1024 = 73400320$ Bytes --> echo 73400320 > memory.max
CPU Limit (1 Core): Set the Quota equal to the Period (100000 microseconds) --> echo "100000 100000" > cpu.max

## 💀 Task 4: Bonus - The OOM Killer
In this task, I demonstrated how the Linux Kernel handles a container that exceeds its allowed memory usage (Out Of Memory).

Scenario:
Created a container named memory-eater.

Set a hard limit of 70MB RAM and disabled Swap (--memory-swap 70m).

Executed a command to consume more than 70MB of RAM immediately.

Result:
The container was immediately killed by the system.

![OOM](https://github.com/OmarHesham249/Docker-K8S-Labs/blob/main/Lab1/Screenshots/Flooding%20the%20memory%20and%20OOM%20Killer.png)

Status: Exited (137)

Exit Code 137: Indicates SIGKILL (9) + 128, confirming the OOM Killer action.
