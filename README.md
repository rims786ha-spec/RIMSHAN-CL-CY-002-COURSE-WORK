# RIMSHAN-CL-CY-002-COURSE-WORK
CL-CY-002-REPORT

# Task 1: Git Version Control and Collaborative GitHub Workflow

## 1. Understanding Git and Version Control

Git is a distributed version control system used to track changes in source code and maintain different versions of a project. GitHub is a platform used to host Git repositories and collaborate with developers through branches and Pull Requests.

Important concepts used in this task include repositories, commits, branches, remotes, Pull Requests, merge conflicts, rebase, revert, cherry-pick, and Git configuration.

Git was verified using:

```bash
git --version
```

Git version used: `2.53.0`

Git identity was configured using:

```bash
git config --global user.name "*****"
git config --global user.email "*****"
```

Additional Git configurations and aliases were also created to customize the development workflow.

## 2. Creating, Cloning and Managing the Repository

Created a GitHub repository named `git-workflow-practice` and cloned it to the Ubuntu system using:

```bash
git clone <repository-url>
cd git-workflow-practice
```

The remote repository was verified using:

```bash
git remote -v
```

A small project was created and modified locally to practise the Git workflow. The changes were checked, staged, committed, and pushed to GitHub using:

```bash
git status
git diff
git add .
git commit -m "Add Git workflow revision notes"
git push
```

This demonstrated the complete workflow from local development to the remote GitHub repository.

## 3. Branching and Pull Requests

A feature branch was created to keep development work separate from the `main` branch:

```bash
git switch -c feature/about-git
```

Changes were made on the feature branch and pushed to GitHub using:

```bash
git add .
git commit -m "Add project description"
git push -u origin feature/about-git
```

A Pull Request was created from the feature branch to the `main` branch. The changes were reviewed and merged successfully.

The workflow followed was:

```text
Feature Branch → Commit → Push → Pull Request → Review → Merge
```

## 4. Merge Conflicts and Git Rebase

A merge conflict was intentionally created by making different changes to the same part of a file in two branches. Git was unable to automatically combine the changes and marked the conflicting section.

The conflict was identified using:

```bash
git status
```

The conflicting content was manually corrected and staged. Git rebase was then used to apply the feature branch changes on top of the latest `main` branch:

```bash
git rebase main
```

After resolving the conflict, the rebase was continued using:

```bash
git add <file>
git rebase --continue
```

This provided practical understanding of merge conflicts, conflict resolution, and the use of Git rebase.
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-03%2007-33-21.png)

## 5. Git Revert and Cherry-Pick

The `git revert` command was practised to safely undo the changes introduced by an earlier commit:

```bash
git revert <commit-id>
```

Git created a new commit that reversed the changes while preserving the existing project history.

The `git cherry-pick` command was also practised to apply a specific commit from another branch:

```bash
git cherry-pick <commit-id>
```

This demonstrated how an individual change can be transferred between branches without merging the complete branch.
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-03%2007-31-48.png)

## 6. Customized Git Workflow

Git configuration was customized using `git config`. The default branch was configured as `main`, and aliases were created for frequently used commands:

```bash
git config --global init.defaultBranch main
git config --global alias.st status
git config --global alias.br branch
git config --global alias.cm "commit -m"
git config --global alias.lg "log --oneline --graph --decorate --all"
```

These configurations simplified frequently used Git commands and created a customized Git workflow.
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-03%2007-30-51.png)

## 7. Open-Source Contribution

Contributed to the `lingdojo/kana-dojo` open-source project by adding a Japan-related fact through a fork, feature branch, commit, push, and Pull Request workflow.

## 8. Outcome

Successfully learned and practised Git version control and GitHub collaboration, including repository cloning, commits, remote repositories, branch management, Pull Requests, merge conflict resolution using rebase, `git revert`, `git cherry-pick`, customized Git configuration, and an open-source contribution.

The task provided practical experience in managing project changes and following a collaborative Git workflow from local development to GitHub.

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


# Task 8: Use Kubernetes Secrets and Environment Variables

## 1. Understanding Kubernetes ConfigMaps and Secrets

Kubernetes ConfigMaps and Secrets are used to manage application configuration separately from container images and Deployment YAML files.

**Important components used in this task:**

- **Namespace:** A logical workspace used to organize Kubernetes resources. I created the `secrets-lab` namespace.
- **ConfigMap:** Stores non-sensitive configuration data such as application settings and AWS region.
- **Secret:** Stores sensitive information such as AWS access keys and session tokens.
- **Deployment:** Manages application Pods and maintains the desired number of replicas.
- **Environment Variables:** Allow containers to access configuration and credentials at runtime.
- **Volume Mount:** Makes ConfigMap data available as files inside a container.

## 2. Creating and Applying the ConfigMap

Created a ConfigMap named `app-config` in the `secrets-lab` namespace.

The ConfigMap contained application configuration, including `APP_NAME`, `APP_ENV`, and `AWS_DEFAULT_REGION`. The AWS region was configured as `ap-south-1`.

Created a Deployment named `config-demo` using the `nginx:stable` image. Configured the Deployment to consume ConfigMap values through environment variables and mount the ConfigMap as a read-only volume at `/etc/app-config`.

During configuration, I encountered a volume mounting error because the volume referenced in `volumeMounts` was not defined under the Pod's `volumes` section. I corrected the YAML and successfully applied the Deployment.
![ConfigMap](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-02%2013-24-20.png)

## 3. Creating the Kubernetes Secret

Created a Kubernetes Secret named `aws-credentials` to store AWS credentials without hardcoding them into the application configuration.

The Secret contained the following credentials:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`

I updated the credentials after encountering an authentication error with my previous AWS account.

Verified the AWS credentials using the AWS CLI command:

```bash
aws sts get-caller-identity
```

The command successfully returned the AWS identity associated with the configured credentials.

## 4. Configuring Environment Variables

Configured Kubernetes environment variables to obtain AWS credentials from the `aws-credentials` Secret using `secretKeyRef`.

The AWS region was provided through the ConfigMap.

This allowed the application container to access the required configuration and AWS credentials without directly hardcoding sensitive values in the Deployment.

## 5. Testing AWS S3 Access from Kubernetes

Created a temporary Pod named `aws-cli-test` using the `amazon/aws-cli` container image.

Configured the Pod to consume AWS credentials from the Kubernetes Secret as environment variables.

Initially, the AWS CLI returned an `InvalidClientTokenId` error due to invalid credentials. After updating the credentials and Kubernetes Secret, the authentication issue was resolved.

Used the AWS CLI to access Amazon S3 from inside the Kubernetes Pod. The test successfully listed the `s3-test.txt` file stored in the S3 bucket.

This verified that the Kubernetes Pod could authenticate with AWS and access S3 using credentials provided through the Kubernetes Secret.

## 6. Verifying the Deployment

Checked the Deployment status using:

```bash
kubectl get deployments -n secrets-lab
```

The `config-demo` Deployment showed **1/1 replicas ready and available**.

Verified the Secret references in the Deployment using:

```bash
kubectl get deployment config-demo -n secrets-lab \
-o jsonpath='{range .spec.template.spec.containers[*].env[*]}{.name}{" : "}{.valueFrom.secretKeyRef.name}{"\n"}{end}'
```

The output confirmed that `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_SESSION_TOKEN` referenced the `aws-credentials` Secret.

Also verified that the ConfigMap was mounted inside the Nginx container and that its configuration could be read from `/etc/app-config`.

![Secret](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-02%2013-29-02.png)
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-02%2013-29-40.png)

## Outcome

Successfully created and applied a Kubernetes ConfigMap and Secret, configured a Deployment to use environment variables and mounted configuration files, and verified the Deployment status. Tested AWS authentication from a Kubernetes Pod and successfully accessed Amazon S3 using credentials stored in a Kubernetes Secret.

This task demonstrated how to separate sensitive credentials from application configuration and securely provide them to Kubernetes workloads. The S3 file was uploaded separately from the Ubuntu terminal, while the Kubernetes Pod was used to verify S3 access.

# Task 9: Deploy an Application to Push Files from Kubernetes to AWS S3

## 1. Objective

To build and containerize a file-upload web application, deploy it on Minikube using Kubernetes, securely provide AWS credentials through Kubernetes Secrets, and upload files to an Amazon S3 bucket. This task integrates Docker, Kubernetes, AWS IAM, S3, and Secrets into a complete cloud deployment pipeline.

## 2. Technologies Used

- **Python Flask:** To develop the file-upload web application.
- **Docker:** To containerize the application.
- **Kubernetes:** To deploy and manage the application.
- **Minikube:** To run a local Kubernetes cluster.
- **Kubernetes Secrets:** To store AWS credentials and inject them into the application.
- **AWS IAM:** To provide credentials and permissions for accessing AWS services.
- **Amazon S3:** To store uploaded files.
- **Boto3:** Python SDK used by the backend to communicate with AWS S3.

## 3. Building the File-Upload Application

Developed a simple web application using Flask with a file picker and an Upload button. The backend receives the selected file and uses the Boto3 library to upload it to the configured Amazon S3 bucket.

The application was tested locally, and files were successfully uploaded to S3.

## 4. Containerizing the Application Using Docker

Created a Docker image of the Flask application to package the application code, dependencies, and runtime environment.

Built the Docker image using the following command:

```bash
docker build -t s3-file-upload:1.0 .
```

The image was tested by running the application inside a Docker container. The file-upload functionality was verified successfully.

## 5. Loading the Image into Minikube

Started Minikube and loaded the locally built Docker image into its environment.

```bash
minikube status
minikube start
minikube image load s3-file-upload:1.0
```

Verified that the image was available inside Minikube.

```bash
minikube image ls | grep s3-file-upload
```

This allowed Kubernetes to use the local image without downloading it from a remote container registry.

## 6. Creating Kubernetes Secrets

Created a Kubernetes Secret named `s3-aws-credentials` in the `secrets-lab` namespace to store the AWS access key ID and secret access key.

```bash
kubectl create secret generic s3-aws-credentials \
  -n secrets-lab \
  --from-literal=AWS_ACCESS_KEY_ID="$AWS_ACCESS_KEY_ID" \
  --from-literal=AWS_SECRET_ACCESS_KEY="$AWS_SECRET_ACCESS_KEY"
```

Updated the existing Secret with the correct credential values and verified it using:

```bash
kubectl describe secret s3-aws-credentials -n secrets-lab
```

Both credential entries were confirmed to contain nonzero values. The credentials were kept separate from the application code and Docker image.

## 7. Deploying the Application on Kubernetes

Created a `deployment.yaml` file to define the application Deployment.

The configuration specified the Docker image, one replica, container port 5000, and the environment variables required by the application. AWS credentials were injected using Kubernetes `secretKeyRef`.

The image pull policy was set to `Never` because the image was already loaded into Minikube.

Applied the Deployment:

```bash
kubectl apply -f deployment.yaml
```

Verified the Deployment and Pod:

```bash
kubectl get deployments -n secrets-lab
kubectl get pods -n secrets-lab
kubectl rollout status deployment/s3-file-upload -n secrets-lab
```

The application was successfully deployed and its Pod was verified.

## 8. Exposing the Application Through a Kubernetes Service

Created a NodePort Service to make the application accessible through a browser.

```bash
kubectl expose deployment s3-file-upload \
  --name=s3-file-upload-service \
  --type=NodePort \
  --port=80 \
  --target-port=5000 \
  -n secrets-lab
```

Retrieved the application URL using:

```bash
minikube service s3-file-upload-service \
  -n secrets-lab --url
```

Opened the generated URL in a web browser and accessed the file-upload interface.

## 9. Uploading and Verifying Files in Amazon S3

Selected a test file through the application's web interface and clicked the Upload button.

The Flask backend received the file and used Boto3, along with the AWS credentials injected by Kubernetes, to upload it to the configured S3 bucket.

The application displayed a successful upload message. The uploaded object was then verified using the AWS CLI:

```bash
aws s3 ls s3://marvel-task-2026-1/ --recursive
```

The uploaded file appeared in the S3 bucket, confirming that the complete upload process worked successfully.

## 10. Outcome

Successfully built and containerized a Flask file-upload application, deployed it on Minikube, configured Kubernetes Secrets for AWS credentials, and exposed the application through a NodePort Service. Files were uploaded through the web interface and verified in Amazon S3.
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-02%2013-11-09.png) 
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-02%2013-11-21.png)
![](https://raw.github.com/rims786ha-spec/RIMSHAN-CL-CY-002-COURSE-WORK/main/Screenshot%20From%202026-10-02%2013-32-36.png)


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

