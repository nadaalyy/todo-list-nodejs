# Todo List Node.js – DevOps Task

## Part 1 - Dockerize the application, CI Pipeline with Docker and GitHub Actions

###  Step 1: Clone the Repository
- Started by cloning the following repository to my local machine:https://github.com/Ankit6098/Todo-List-nodejs

### Step 2: Configure MongoDB
- Created a MongoDB cluster using MongoDB Atlas.  
Then, update the `.env` file in the project with my MongoDB URI:

### Step 3: Dockerize the Application
- Created a `Dockerfile` to containerize the Node.js app.  
Then, built and tested the Docker image (node-app) locally:

![Dockerize the Application](https://github.com/user-attachments/assets/22bfa327-5447-40b7-94ec-c051413f93ef)


![Dockerize the Application](https://github.com/user-attachments/assets/d5ff5322-1494-45f2-943d-7958de0cd42b)

- After that, tested the image by running a container named "node-app-container"

![Dockerize the Application](https://github.com/user-attachments/assets/b280ac74-d982-4b41-9130-ae9174f211d8)

![Dockerize the Application](https://github.com/user-attachments/assets/70f84657-2f9d-4100-9b71-26430a750cd1)

- The container also appears as running in Docker Desktop, confirming that the app is successfully containerized and deployed.

![Dockerize the Application](https://github.com/user-attachments/assets/a1f112ab-3a7c-4c03-8173-8fcf16310410)

- The application became accessible at :http://localhost:4000
  
![Dockerize the Application](https://github.com/user-attachments/assets/905536ef-4317-4dfe-ae73-e713f04ec8e4)

### 🔹 Step 4: GitHub Actions to create a CI pipeline
- Created a docker repository on Docker Hub.  
- Used GitHub Actions to create a CI pipeline that builds the image and pushes it to
- Used the `docker.yml` file in the CI/CD pipeline to build and push the Docker image to Docker Hub
a private docker registry.

![Dockerize the Application](https://github.com/user-attachments/assets/b2b26ebe-32a1-4ad7-a4f0-b1bfa77bed4e)


- At the end of Part 1, I had a working CI pipeline that pushes the updated Docker image to a the registry automatically whenever I push changes to the GitHub repo.

![Dockerize the Application](https://github.com/user-attachments/assets/ecc0bc93-b4ad-4607-ac32-0bec186cbbcc)



## Part 2 - Creating a Linux VM on your local machine and using Ansible to configure the machine

###  Step 1: Creating the Red Hat Linux VM
- Created a Red Hat Linux virtual machine on my local machine using vmware
- The VM was configured with the IP address and SSH access enabled (the IP address of the VM is: 192.168.72.128)

###  Step 2: Setting Up Ansible on Local Machine
- Installed Ansible on my local machine (the control node)
- Created an inventory file `inventory.ini` with the IP address and SSH details of the VM

![Dockerize the Application](https://github.com/user-attachments/assets/00034040-5c72-4249-aced-b040293bb951)

 ###  Step 3: Writing the Ansible Playbook
 - Created a playbook file `setup-docker.yml` to automate the configuration steps
 - The playbook installs required packages, adds Docker repository, and installs Docker on the Red Hat VM.
 - Ran the Ansible playbook:
   
 ![Dockerize the Application](https://github.com/user-attachments/assets/e61601e7-9f7c-4d9e-a629-5d079a3b016e)
 
- Verified that Docker was installed and running successfully on the VM:
  
![Dockerize the Application](https://github.com/user-attachments/assets/fa6239b5-1389-407d-bb33-00da4f56f11b)

![Dockerize the Application](https://github.com/user-attachments/assets/ddc4f990-431d-47fb-b7c3-421a53705c2f)


## Part 3 - Running the Application with Docker Compose and Auto-Update

 ###  Step 1:  Preparing the Application on the VM
 - Created the `docker-compose.yml`file that defines the required services and containers

###  Step 2:  Running Docker Compose
 - Pulling the image and starting the container :

![Dockerize the Application](https://github.com/user-attachments/assets/93238c49-2ef9-4056-a78f-feee3d322b5c)

###  Step 3: Enabling Continuous Image Update and health check :
- To continuously check for changes in the image on the Docker registry, I chose Watchtower as the update automation tool:
- Pulled the Watchtower image,ran Watchtower as a container, monitoring all running containers.The setup checks for new images every 30 seconds and updates the containers if any changes are found.

![Dockerize the Application](https://github.com/user-attachments/assets/cad83ead-57b7-4bcb-ac57-ec3a4b9f52b6)

- Accessed the running application via browser using the public IP of the RedHat VM on port 4000 to confirm that it's working properly:
  
![Dockerize the Application](https://github.com/user-attachments/assets/760bd8a8-ee66-49e4-b9b3-35ec46e0ce30)

## Part 4 - Running the same Node.js application using Kubernetes instead of Docker Compose

 ###  Step 1:  Install Kubernetes (Minikube)
- On the RedHat VM, Minikube was installed (a local Kubernetes cluster tool) to set up a single-node Kubernetes environment.
- kubectl was also installed to interact with the cluster.

 ###  Step 2:  Creating `todo-deployment.yml` and `todo-service.yml` files

  - Created  `todo-deployment.yml` file to define a Deployment for the Node.js app.It specifies the image, number of replicas, and container port.
  - Created  `todo-service.yml` file to expose the Node.js app using a NodePort.
  - Accessing the Node.js app in the browser using the VM’s IP address and the exposed NodePort:

![Dockerize the Application](https://github.com/user-attachments/assets/e363de46-06b8-47b7-a8e4-e7415436dd8b)


