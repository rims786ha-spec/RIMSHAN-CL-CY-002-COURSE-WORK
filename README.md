# RIMSHAN-CL-CY-002-COURSE-WORK
CL-CY-002-REPORT


# Task 2: Docker Basics and Container Management

## 1. Understanding Docker and Containers

Docker is a containerization platform that allows applications to run in isolated environments called containers.

Important concepts learned:

* **Docker Image:** Template used to create containers.
* **Docker Container:** Running instance of an image.
* **Docker Hub:** Repository for Docker images.
* **Docker CLI:** Command-line tool used to manage Docker resources.

### Containers vs Virtual Machines

* Containers are lightweight and share the host operating system.
* Virtual Machines include a complete operating system and require more resources.
* Containers start faster and consume less memory.

---

## 2. Pulling and Running a Docker Image

Downloaded the Nginx image from Docker Hub:

```bash
docker pull nginx
```

Started a container from the image:

```bash
docker run -d -p 8080:80 nginx
```

![Image download and Running conatainer](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%202026-06-07%20042314.png)
![Nginx server](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%202026-06-07%20044705.png)


---

## 3. Viewing Containers and Logs

Checked running containers:

```bash
docker ps
```

Viewed all containers, including stopped containers:

```bash
docker ps -a
```

Viewed container logs:

```bash
docker logs <container_id>
```

![Container list and logs](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Container1.png)


---

## 4. Inspecting and Managing Containers

Inspected container details:

```bash
docker inspect <container_id>
```

Stopped and restarted the container:

```bash
docker stop <container_id>
docker restart <container_id>
```

Removed the container:

```bash
docker rm <container_id>
```


---

## 5. Managing Docker Images

Listed available images:

```bash
docker images
```

Removed an unused image:

```bash
docker rmi <image_name>
```


---

## Outcome

Successfully learned Docker fundamentals, understood the difference between Containers and Virtual Machines, pulled images from Docker Hub, created and managed containers, viewed logs and container details, listed images, and performed complete container lifecycle management using Docker CLI commands.



# Task 3: Containerizing a Notes Application Using Docker

## 1. Understanding Docker and Containerization

Docker is a containerization platform that allows developers to package applications along with their dependencies into portable containers. Containers ensure that applications run consistently across different environments without requiring additional configuration.

Important components used in this task:

* **Dockerfile:** A text file containing instructions to build a Docker image.
* **Docker Image:** A packaged blueprint containing the application and its dependencies.
* **Docker Container:** A running instance of a Docker image.
* **Port Mapping:** Allows access to services running inside a container from the host machine.
* **Image Layers:** Each Dockerfile instruction creates a separate layer that Docker can cache and reuse.

---

2. Creating the Notes Application

A simple Notes Application was developed using Node.js and Express.

Features implemented:

Add new notes.
View saved notes.
Delete existing notes.
Store notes in a local JSON file.

Project structure:

notes-app/
│
├── public/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── notes.json
├── server.js
├── package.json
└── Dockerfile

The application was configured to run on Port 3000 and successfully served both the frontend and backend functionality.
![Note App](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Note%20app.png)

---

## 3. Writing the Dockerfile

A Dockerfile was created to define the environment required for the application.

Example Dockerfile:

FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]


### Dockerfile instructions used:

 * **FROM**– Selects the base Node.js image.

 * **WORKDIR** – Sets the working directory inside the container.

 * **COPY** – Copies project files into the container.

 * **RUN** – Installs required dependencies.

 * **EXPOSE** – Documents the application port.

* **CMD** – Starts the application when the container runs.


## 4. Building the Docker Image

The Docker image was built using the following command:

```bash
docker build -t notes-app .
```


Docker successfully processed the Dockerfile instructions and created the application image.

The image was verified using:


docker images

Docker Image's Image
![Docker Image](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Doker%20Image.png)

---

## 5. Running the Docker Container

A container was launched from the created image using:

```bash
docker run -d -p 3001:3000 --name notes-container notes-app
```

Explanation:

* `-d` runs the container in detached mode.
* `-p 3001:3000` maps host port 3001 to container port 3000.
* `--name` assigns a name to the container.

The running container was verified using:

```bash
docker ps
```

Running Docker Container Image.
![Running Docker container](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Container.png)

---

## 6. Accessing the Application

The Notes Application was accessed through a web browser using:

http://localhost:3001

The application loaded successfully and all note management features were tested.

Verified operations:

Adding notes.
Viewing notes.
Deleting notes.

The frontend communicated successfully with the Node.js and Express backend, and notes were stored and retrieved from the local JSON file.



Notes Application running in browser on Port 3001.
![Note app](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/fn.png)
---

## 7. Understanding Docker Image Layers

Each instruction in the Dockerfile creates a separate image layer.

Example:

FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

CMD ["node", "server.js"]


  ### Generated layers:

Base Node.js image.
Working directory creation.
Package file copy.
Dependency installation.
Application source code copy.
Application startup command.

Docker caches unchanged layers, which speeds up future image builds.

 Docker build output showing image layers.
 ![Image Layer](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Image%20layer.png)

---

## Outcome

Successfully containerized a Notes Application using Docker by creating a Dockerfile, building a Docker image, running the application inside a container, mapping container ports to the host machine, and accessing the application through a web browser. Additionally, gained practical understanding of Docker images, containers, port mapping, and image layers.




# Task 4: Launch and Manage an AWS EC2 Instance

## 1. Understanding EC2

Amazon EC2 (Elastic Compute Cloud) is a cloud computing service provided by AWS that allows users to create and manage virtual machines on the cloud. These virtual machines can host applications, websites, and services that are accessible over the internet.

Important components used in this task:

* **AMI (Amazon Machine Image):** Contains the operating system required to launch an EC2 instance. I used Ubuntu Server 24.04 LTS.
* **Instance Type:** Determines CPU and memory allocation. I selected a t3.micro instance.
* **Security Group:** Acts as a firewall and controls inbound and outbound traffic.
* **Key Pair:** Used for secure authentication while connecting through SSH.

---

## 2. Launching the EC2 Instance

* Opened the AWS EC2 dashboard.
* Launched a new Ubuntu EC2 instance.
* Selected the t3.micro instance type.
* Created and downloaded a `.pem` key pair.
* Successfully launched the EC2 instance.

 EC2 instance in Running state.
![EC2 instance in Running state](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/EC2%20instance%20in%20Running%20state.png)
---

## 3. Connecting to the EC2 Instance

* Connected to the EC2 instance using SSH from Windows PowerShell.
* Authenticated using the downloaded `.pem` key.
* Verified successful login to the Ubuntu server.

This provided command-line access to the cloud server.

 Successful SSH connection showing the Ubuntu terminal.
 ![SSH Connection](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/SSH%20connection.png)

---

## 4. Installing and Starting Nginx

Installed the Nginx web server using the following commands:

```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl status nginx
```

The Nginx service started successfully and was verified using the status command.

 Nginx status showing "active (running)".
 ![Nginx Status](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Nginx%20status%20showing%20active.png)

---

## 5. Configuring Security Group Rules

Initially, the Nginx page was not accessible because HTTP traffic was blocked.

To resolve this:

* Opened the Security Group attached to the EC2 instance.
* Added an inbound rule for HTTP.
* Allowed traffic on Port 80 from Anywhere (0.0.0.0/0).

This enabled public access to the web server.

 

---

## 6. Verifying the Web Server

Opened the EC2 public IP address in a web browser:

```text
http://98.130.124.189
```

The default Nginx welcome page was displayed successfully, confirming that the web server was running and accessible from the internet.

 Nginx Welcome Page.
 ![ Nginx Welcome Page](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Nginx%20Welcome%20Page.png)


---

## Outcome

Successfully launched and managed an AWS EC2 instance, connected through SSH, installed Nginx, configured Security Groups, and hosted a web server accessible through the public IP address.
# Task 5: Create and Manage a Kubernetes Pod using Minikube

## 1. Understanding Kubernetes

Kubernetes is a container orchestration platform used to deploy and manage containerized applications. For this task, Minikube was used to run Kubernetes locally, while `kubectl` was used to communicate with and manage the cluster.

**Important concepts used in this task:**

- **Cluster:** The complete Kubernetes environment.
- **Node:** A machine that runs Kubernetes workloads.
- **Pod:** The smallest deployable unit in Kubernetes that contains one or more containers.
- **Control Plane:** Manages and controls the Kubernetes cluster.
- **kubectl:** Command-line tool used to interact with Kubernetes.

## 2. Starting the Minikube Cluster

Started the local Kubernetes cluster using:

```bash
minikube start --driver=docker
```

The cluster status was checked using:

```bash
minikube status
```

The available Node was verified using:

```bash
kubectl get nodes
```

The Minikube Node was successfully shown in the `Ready` state.

> **Minikube cluster and Node running successfully.**

## 3. Creating the Kubernetes Pod

Created a YAML manifest file named `nginx-pod.yaml` to define the Pod configuration.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx
```

The manifest specifies an Nginx container using the Nginx image. Kubernetes automatically pulls the image if it is not already available on the Node.

> **Nginx Pod YAML manifest created successfully.**

## 4. Deploying the Pod

Applied the YAML manifest to the Kubernetes cluster using:

```bash
kubectl apply -f nginx-pod.yaml
```

The Pod was successfully created by Kubernetes.

The Pod status was verified using:

```bash
kubectl get pods
```

The output showed:

```
nginx-pod   1/1   Running
```

This confirmed that the Nginx container was successfully running inside the Pod.

> **Nginx Pod successfully deployed and running.**
![successfully deployed pod](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-10%2016-39-50.png)

## 5. Inspecting the Pod

Detailed information about the Pod was obtained using:

```bash
kubectl describe pod nginx-pod
```

This displayed the Pod's Node, container, image, status, IP address, and events, helping verify the configuration and troubleshoot any issues.

> **Pod details successfully displayed using `kubectl describe`.**
![describe](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-10%2016-24-55.png)

## 6. Viewing Pod Logs

The logs generated by the Nginx container were checked using:

```bash
kubectl logs nginx-pod
```

This command was used to view the output generated by the container and verify its runtime information.

> **Nginx Pod logs successfully accessed using `kubectl logs`.**
![logs](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-10%2016-40-52.png)

## Outcome

Successfully created and deployed an Nginx Pod on a local Minikube Kubernetes cluster using a YAML manifest. Verified the Kubernetes Node and Pod status, inspected the Pod configuration using `kubectl describe`, and accessed the container logs using `kubectl logs`. The Pod reached the `1/1 Running` state, confirming successful deployment and execution.


# Task 6: Manage AWS S3 and IAM with CLI

## 1. Objective

The objective of this task was to understand AWS IAM, S3, and AWS CLI, configure CLI access on Ubuntu, and manage S3 storage using command-line operations.

## 2. IAM Concepts

AWS IAM (Identity and Access Management) controls access to AWS resources.

The following concepts were studied:

- **Users** – Individual identities with permissions.
- **Groups** – Collections of users with common permissions.
- **Roles** – Temporary permissions used by users or AWS services.
- **Policies** – Define allowed or denied actions.
- **Least Privilege** – Giving only the permissions required.
![IAM user](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-10%2021-15-21.png)
## 3. AWS CLI Configuration

AWS CLI was already installed on Ubuntu and verified using:

```
aws --version
```

The CLI was configured using:

```
aws configure
```

The IAM user's Access Key, Secret Access Key, region `ap-south-1`, and JSON output format were configured.

AWS connectivity was verified using:

```
aws sts get-caller-identity
```
![aws config](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/aws%20config.png)


## 4. S3 Bucket Creation

An S3 bucket was created from the Ubuntu terminal using:

```
aws s3api create-bucket \
  --bucket YOUR-BUCKET-NAME \
  --region ap-south-1 \
  --create-bucket-configuration LocationConstraint=ap-south-1
```

The bucket was verified using:

```
aws s3 ls
```

![Bucket Creation](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-10%2023-15-31.png)

## 5. S3 Object Management

A test file was created:

```
echo "Hello from AWS S3" > test.txt
```

**Upload**

```
aws s3 cp test.txt s3://YOUR-BUCKET-NAME/
```

**List Objects**

```
aws s3 ls s3://YOUR-BUCKET-NAME/
```

**Download**

```
aws s3 cp s3://YOUR-BUCKET-NAME/test.txt ./s3-download/
```

**Delete**

```
aws s3 rm s3://YOUR-BUCKET-NAME/test.txt
```

The object was successfully uploaded, listed, downloaded, and deleted.

![management](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-10%2023-16-16.png)
## 6. Least-Privilege IAM Policy

A custom IAM policy was created to restrict access to the specific S3 bucket.

The policy allowed:

```
s3:ListBucket
s3:GetObject
s3:PutObject
s3:DeleteObject
```

Access to other S3 buckets was restricted, demonstrating the Principle of Least Privilege.


![IAM Policy](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-12%2001-01-23.png)![IAM policy](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-12%2001-01-40.png)
## 7. Learning Outcomes

- Learned IAM users, groups, roles, and policies.
- Configured AWS CLI on Ubuntu.
- Created and managed an S3 bucket using CLI.
- Uploaded, listed, downloaded, and deleted S3 objects.
- Verified AWS authentication using CLI.
- Applied a least-privilege IAM policy.

## 8. Conclusion

The task provided practical experience with AWS IAM, S3, and AWS CLI. It demonstrated how IAM controls access and how S3 resources can be securely managed through the command line using least-privilege permissions.




# Task 7: Kubernetes Deployments and Services

## 1. Understanding Kubernetes Deployment

A Kubernetes Deployment is used to manage and maintain multiple replicas of an application. It ensures that the required number of Pods are running and provides features such as scaling and rolling updates.

In this task, an NGINX application was deployed using a YAML manifest with 3 replicas.

## 2. Creating Deployment YAML

A `deployment.yaml` file was created to define the NGINX Deployment.

The Deployment used:

- NGINX 1.27 container image
- 3 replicas
- Container port 80
- CPU and memory resource requests and limits
- Readiness probe to check whether the application is ready
- Liveness probe to check whether the application is healthy

The Deployment was created using:

```
kubectl apply -f deployment.yaml
```

The running Pods were verified using:

```
kubectl get pods
```
![Deployment](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/WhatsApp%20Image%202026-08-12%20at%2001.22.17.jpeg)
## 3. Creating ClusterIP Service

A ClusterIP Service was created to expose the NGINX application internally within the Kubernetes cluster.

The service was configured to forward traffic from port 80 to the NGINX containers.

It was deployed using:

```
kubectl apply -f service-clusterip.yaml
```

The Service was verified using:

```
kubectl get services
```
![clusterIP](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-11%2023-56-59.png)
## 4. Creating NodePort Service

A NodePort Service was created to make the NGINX application accessible from outside the Kubernetes cluster.

The service used NodePort 30080 and forwarded traffic to port 80 of the NGINX Pods.

It was deployed using:

```
kubectl apply -f service-nodeport.yaml
```

The service was checked using:

```
kubectl get services
```

The application was accessed through Minikube using:

```
minikube service nginx-nodeport --url
```

The generated URL was opened in a browser, displaying the NGINX Welcome Page, confirming successful external access.
![Nodeport](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-11%2023-58-14.png)

## 5. Scaling the Deployment

The Deployment was scaled from 3 replicas to 5 replicas using:

```
kubectl scale deployment nginx-deployment --replicas=5
```

The Pods were verified using:

```
kubectl get pods
```

The Deployment was then scaled down from 5 replicas to 2 replicas:

```
kubectl scale deployment nginx-deployment --replicas=2
```

This demonstrated Kubernetes' ability to dynamically scale applications up and down according to requirements.

## 6. Verification

The final Kubernetes resources were verified using:

```
kubectl get deployments
kubectl get pods
kubectl get svc
```

The verification confirmed that the Deployment, Pods, ClusterIP Service, and NodePort Service were created successfully.

## 7. Result

The Kubernetes Deployment and Services were successfully configured using YAML manifests. The NGINX application was deployed with multiple replicas, exposed internally using ClusterIP, and made accessible externally using NodePort. The application was successfully accessed through a browser, and the Deployment was scaled up and down using `kubectl`.
![NGINX](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-08-11%2023-59-52.png)


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------




# Cyber Security

# A Fundamentals of Computer Networking
## Introduction
A network is a system in which multiple entities or devices are interconnected to communicate and share resources. Networks exist in everyday life, such as transportation systems, electricity grids, postal services, and social connections. In computing, networks connect devices such as computers, smartphones, security cameras, and smart machines. Networks can range from a small connection between two devices to the global Internet connecting billions of devices. They play an essential role in areas such as communication, weather monitoring, electricity management, and traffic control. Understanding computer networks is also fundamental to cybersecurity and modern technology.

## Internet 
The Internet originated with **ARPANET**, a U.S. Defence Department-funded project developed in the late 1960s as an early working network. In **1989, Tim Berners-Lee introduced the World Wide Web (WWW)**, enabling information to be stored and shared through the Internet. The Internet can be understood as a **network of networks**, connecting millions of smaller networks worldwide. Networks can be classified into **private networks** and **public networks**, with the Internet being the largest public network. Devices communicate with each other using unique **network addresses** for identification. A public network connects multiple private networks globally to enable worldwide communication and resource sharing.

## IP Address
Devices on a network are identified using **IP addresses** and **MAC addresses**, similar to a name and fingerprint. An **IP address** identifies a device on a network and can change, while a **MAC address** uniquely identifies its network interface. **Private IP addresses** are used within local networks, whereas **public IP addresses** enable devices to communicate over the Internet. **IPv4** provides about 4.3 billion addresses, while **IPv6** was introduced to overcome address limitations. MAC addresses can be manipulated through **MAC spoofing**, making MAC-based security alone unreliable. The **Internet is a public network that connects multiple private networks globally**. 


## Ports
Network ports are numbered communication channels that control how data enters and leaves a device. Ports range from **0 to 65,535**, with ports **0–1024** known as well-known ports used by standard services. Common examples include **HTTP (80), HTTPS (443), FTP (21), SSH (22), SMB (445), and RDP (3389)**. Port numbers are standardized to help applications communicate correctly, but services can operate on alternative ports such as **8080**. When a non-standard port is used, the port number must be specified explicitly in the address. Understanding ports is essential for network communication, service management, and cybersecurity.

## Packets & Frames 
Packets and frames are fundamental units of data transmission that operate at different layers of the **OSI model**. A **packet** operates at the **Network Layer (Layer 3)** and contains IP addressing and payload data, while a **frame** operates at the **Data Link Layer (Layer 2)** and encapsulates the packet with MAC addresses. Large messages are divided into smaller packets to improve network efficiency, reduce congestion, and support reliable transmission. The process of adding headers and wrapping data as it moves through OSI layers is called **encapsulation**. Important packet header fields include **source and destination addresses, checksum, and TTL**, which assist in routing, integrity verification, and preventing endless circulation.

## Networking Devices
Networking devices are essential hardware components that facilitate communication, traffic management, connectivity, and security across networks. A **switch** forwards frames using MAC addresses, while a **hub** broadcasts traffic to all ports and operates in half-duplex mode. **Routers** connect different networks and forward packets based on IP addresses, while **multilayer switches** combine Layer 2 switching and Layer 3 routing using hardware-based processing. Security devices such as **firewalls, IDS/IPS, and VPNs** protect networks by filtering traffic, detecting or preventing threats, and providing encrypted remote access. **Access points** provide wireless connectivity, while advanced devices support efficient inter-VLAN communication and high-speed network performance.

# B Protocols
## DNS
I learned that the **Domain Name System (DNS)** is an essential Internet service that translates human-readable domain names into their corresponding **IP addresses**.
For example, DNS converts a domain such as **google.com** into an IP address such as **142.250.195.78**, allowing devices to locate the required server.
DNS works like the **phonebook of the Internet**, where domain names act like saved contacts and IP addresses represent their phone numbers.
It eliminates the need for users to remember complex numerical IP addresses when accessing websites and online services.
Overall, I understood that DNS plays a crucial role in making Internet communication **simple, user-friendly, and efficient**.

## DHCP

I learned that **DHCP (Dynamic Host Configuration Protocol)** automatically provides devices with essential network settings such as an **IP address, subnet mask, default gateway, and DNS server**.
DHCP is an **application-layer protocol** that uses **UDP ports 67 and 68** and simplifies network configuration for laptops, smartphones, and other devices. I understood the **DORA process — Discover, Offer, Request, and Acknowledge —** through which a client obtains and confirms an IP address lease. Before receiving an IP address, the client uses **0.0.0.0** as its source IP and communicates using broadcast addresses to locate a DHCP server. Finally, I learned that if no DHCP server is available, a device can automatically assign itself an **APIPA (Automatic Private IP Addressing)** address.


## ICMP
I learned that **ICMP (Internet Control Message Protocol)** is primarily used for **network diagnostics, connectivity testing, and error reporting**. I understood that **ping** uses an **ICMP Echo Request (Type 8)** and receives an **Echo Reply (Type 0)** to verify whether a host is reachable and measure **Round-Trip Time (RTT)** and packet loss.
I also learned that **traceroute/tracert** identifies the path taken by packets by using the **TTL (Time-To-Live)** field to control packet traversal across routers. When the TTL reaches zero, the router discards the packet and sends an **ICMP Time Exceeded (Type 11)** message back to the sender. I understood that ICMP tools are valuable for identifying **connectivity problems, network delays, packet loss, and routing paths**, although firewalls or network policies may block ICMP responses.


## HTTP (S)
I learned that **HTTP (HyperText Transfer Protocol)** is the fundamental protocol used for communication between web browsers and web servers to request and deliver web resources. I understood that **HTTPS (HTTP Secure)** is the encrypted version of HTTP, using **SSL/TLS** to protect data and authenticate the communicating website. I learned that **Tim Berners-Lee and his team** developed HTTP, which became a foundation of modern web communication. By using browser Developer Tools and the **Network tab**, I learned how to inspect HTTP requests, including the **request method and server status code**. I also explored **SSL/TLS certificates** and learned how to identify the **Certificate Authority (CA), Common Name (CN), and certificate issuer organization** for different websites.
Overall, I understood how HTTP/HTTPS, encryption, and digital certificates work together to provide **secure and trustworthy web communication**.


## Other Important Models
I learned that the **OSI (Open Systems Interconnection) model** is a theoretical framework that divides network communication into **seven layers**, helping to understand how data travels between devices.
I understood the roles of the **Physical, Data Link, Network, and Transport layers**, where raw bits are transmitted, frames are created, routing is performed, and end-to-end communication is managed.
I learned that **TCP** provides reliable communication using **sequence numbers and error checking**, while **UDP** provides faster communication with less reliability and overhead.
I also understood how **IP operates at the Network layer** for routing data between networks and how protocols such as **HTTP operate at the Application layer**.
The process of adding headers at each layer is called **encapsulation**, and the receiving device removes these headers layer by layer through **decapsulation**.
Overall, I learned that the OSI model is mainly used for **education, networking concepts, troubleshooting, and describing technologies such as L4 and L7 load balancing**.
 
# Windows
## Introduction
I learned how the Windows operating system manages system resources and provides an organized environment for accessing and managing files and applications. I understood File Explorer and the hierarchical folder structure used to efficiently navigate, organize, and locate files. I learned the importance of Windows Updates for fixing security vulnerabilities, improving performance, and resolving bugs and crashes. I also learned how to safely install, update, and uninstall applications, preferably using Microsoft Store or official software websites. Additionally, I understood the difference between Windows Settings and Control Panel, with Control Panel providing access to certain advanced system configurations. Finally, I learned how Task Manager helps monitor processes, CPU, memory, users, detailed processes, and background services.


## Powershell
I learned that PowerShell is a cross-platform automation tool that combines a command-line shell, scripting language, and configuration management framework. I understood that PowerShell is built on the .NET framework and works across Windows, macOS, and Linux. I learned that PowerShell uses objects instead of plain text, where objects contain properties (data) and methods (actions), enabling efficient data handling and automation. I also studied its development by Jeffrey Snover, including the release of PowerShell in 2006 and PowerShell Core in 2016 as an open-source, cross-platform version. Additionally, I learned that PowerShell commands are called cmdlets, which return structured objects and simplify complex system administration and automation tasks.


## Powershell vs CMD
I learned the key differences between Windows Command Prompt (cmd.exe) and PowerShell, including their purpose, capabilities, and use in system administration. Command Prompt is an older command shell primarily designed for running applications, utilities, and basic batch scripts, with limited support for remote administration. In contrast, PowerShell is built on the .NET framework and provides cmdlets for advanced system management, scripting, automation, and remote administration. I learned that PowerShell can manage areas such as the file system, Windows Registry, WMI, Active Directory, users, permissions, and security configurations. I also understood that PowerShell supports Linux and can execute many traditional CMD commands through aliases. Overall, PowerShell offers greater flexibility and is more suitable for complex automation and modern system administration tasks.

## System32
I learned that the Windows directory is the core location containing essential files required for the operating system to function, with C:\Windows being its default path. I understood that Windows can also be installed on a different drive or directory depending on the system configuration. I learned about environment variables, particularly %windir%, which dynamically identifies the location of the Windows directory. These variables store important system information, including operating system paths, processor details, and temporary folder locations. I also learned that the System32 folder contains critical system files and built-in utilities, so modifying or deleting its contents can seriously affect system stability.

## User Accounts & UAC
I learned that Windows primarily provides two types of user accounts: Administrator and Standard User, with different levels of system access and privileges. I understood that an Administrator can make system-wide changes, manage users and groups, install software, and modify system settings, while a Standard User has more limited permissions. I learned that user profiles are stored in C:\Users and are created during the user’s first login through the User Profile Service. I also studied Local Users and Groups Management, which can be accessed using lusrmgr.msc to manage local accounts and groups. Finally, I learned that groups simplify permission management because users inherit the permissions assigned to the groups they belong to.

## Security
I learned about the built-in Windows Security features that help protect systems against malware and other security threats. I understood that Virus & Threat Protection scans for malicious software, App & Browser Control helps block unsafe files and websites, and Device Security provides hardware-level protection. I also learned that regular security scans help identify and address potential threats at an early stage. Additionally, I studied the role of the Windows Firewall, which controls incoming and outgoing network traffic and prevents unauthorized access. I learned that Windows networks can be categorized as Domain, Private, or Public, with Public networks being the least trusted and most vulnerable.

# Linux
## Introduction
I learned that Linux is an open-source and lightweight operating system known for its flexibility, reliability, stability, and efficient performance. It is widely used in web servers, automotive systems, retail Point of Sale (PoS) systems, and critical infrastructure such as traffic control and industrial systems. Linux is available in different distributions (distros), which are customized versions designed for specific requirements and use cases. Popular distributions include Ubuntu and Debian, with Ubuntu being particularly suitable for beginners due to its user-friendly environment. I also learned that Ubuntu can be used as both a desktop operating system and a server platform. Its lightweight nature allows Ubuntu Server to operate efficiently even on systems with limited hardware resources.

## File System
I learned how to create, manage, move, copy, rename, and delete files and directories using essential Linux commands. The touch command is used to create files, while mkdir creates directories, and cp is used to copy files or folders. I learned that the mv command can both move and rename files and directories. The rm command is used to delete files, while the -R option allows directories and their contents to be removed recursively. Finally, I learned to use the file command to identify the actual type and content format of a file, regardless of its file extension

# Others
## Cryptography - Part 1
I learned that cryptography is the practice of protecting information to ensure confidentiality, integrity, and authenticity during digital communication. It is widely used in secure logins, SSH connections, online banking, secure file transfers, and regulatory compliance such as PCI DSS for credit card information. I learned the basic cryptographic concepts of plaintext, ciphertext, cipher, key, encryption, and decryption. Encryption converts plaintext into unreadable ciphertext using a cipher and key, while decryption uses the correct key to recover the original plaintext. The combined use of a cipher and key provides the mechanism for securely transforming data and protecting it from unauthorized access or modification.


## Cryptography - part 2
I learned that cryptography is the practice of protecting information to ensure confidentiality, integrity, and authenticity during digital communication. It is widely used in secure logins, SSH connections, online banking, secure file transfers, and regulatory compliance such as PCI DSS for credit card information. I learned the basic cryptographic concepts of plaintext, ciphertext, cipher, key, encryption, and decryption. Encryption converts plaintext into unreadable ciphertext using a cipher and key, while decryption uses the correct key to recover the original plaintext. The combined use of a cipher and key provides the mechanism for securely transforming data and protecting it from unauthorized access or modification.

# Principles of CyberSecurity 
## CIA
I learned that cyber security focuses on protecting digital systems, networks, applications, and information from cyber threats. The three core principles of cyber security are the CIA Triad: Confidentiality, Integrity, and Availability. Confidentiality ensures that sensitive information is accessible only to authorized users, while Integrity ensures that data remains accurate, complete, and protected from unauthorized modification. Availability ensures that systems, applications, and data remain accessible to authorized users whenever required. I also learned how encryption helps maintain confidentiality and how system failures or website crashes can affect availability. These principles provide a fundamental framework for making informed decisions to protect digital information and systems.

## CIA-Explanantion
I learned that the CIA Triad—Confidentiality, Integrity, and Availability forms the fundamental foundation of cybersecurity and focuses on protecting digital data and services. Confidentiality ensures that sensitive information is accessible only to authorized individuals through mechanisms such as encryption and access controls. Integrity ensures that data remains accurate, trustworthy, and cannot be modified without proper authorization. Availability ensures that systems, data, and services remain accessible to authorized users whenever required, even during failures or high traffic. I also learned how real-world incidents such as stolen credentials, unauthorized changes to transactions, and website outages can compromise these principles. Understanding and maintaining the CIA Triad is essential for protecting information and ensuring secure and reliable digital systems.

# Path 1 - Red Teaming 
I learned that offensive security focuses on actively testing systems from an attacker’s perspective to identify and fix vulnerabilities before real attackers can exploit them. It involves examining exposed components, accessible resources, and how systems respond to unexpected inputs or unusual actions. In this context, hacking refers to ethical and authorized penetration testing, carried out legally and responsibly to strengthen system security. I also learned that offensive security builds on foundational knowledge of computers, networks, and web technologies by applying it from an attacker’s viewpoint. Understanding offensive security terminology and methodologies helps security professionals discover vulnerabilities and assess how multiple weaknesses can be combined to compromise a system. Familiarity with the command-line interface (CLI) is useful for performing practical security tasks and investigations.

# Red Teaming Continuation
I learned that offensive security involves proactively identifying and assessing vulnerabilities before real attackers can exploit them, using authorized and controlled methods. I studied key concepts such as Red Teaming, Penetration Testing, Vulnerability, Exploit, and Scope, and understood that permission and defined scope are essential for conducting ethical security assessments legally. I also learned how security professionals examine web applications to identify hidden or unintentionally exposed pages and resources. Gobuster can be used for automated web directory enumeration, helping testers discover hidden directories and files using a predefined wordlist. Overall, this exercise helped me understand how ethical hackers systematically assess web applications and identify potential weaknesses without causing damage.

