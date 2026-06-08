# Title: Docker Installation and Basic Container Management

## Aim

To understand and implement containerization technology using Docker for developing, deploying, and running applications within isolated containers.

## Objectives

* To gain knowledge of Docker and its role in modern software development.
* To learn the process of installing Docker on a host machine.
* To explore the major Docker components such as Docker Engine, Images, and Containers.
* To practice essential Docker commands for creating and managing containers.
* To evaluate the benefits of Docker in ensuring application portability and environment consistency.

## Theory

Docker is an open-source containerization platform that enables developers to package applications together with all necessary dependencies, libraries, and configurations into lightweight containers. These containers can run consistently across different computing environments, including development, testing, and production systems.

Unlike traditional Virtual Machines (VMs), Docker containers share the host operating system's kernel instead of running a separate operating system. As a result, containers consume fewer system resources such as memory, storage, and CPU power. Docker follows a client-server architecture where the Docker Client communicates with the Docker Daemon (Docker Engine), which is responsible for building, running, and managing containers.

### Key Concepts

**Docker Image:**
A read-only blueprint that contains the application code, libraries, and dependencies required to create containers.

**Docker Container:**
A live and executable instance of a Docker image.

**Dockerfile:**
A text-based configuration file that contains instructions used to build Docker images.

**Docker Hub:**
An online repository that allows users to store, share, and download Docker images.

Docker is widely used in DevOps workflows, cloud environments, microservices architectures, and Continuous Integration/Continuous Deployment (CI/CD) pipelines.

## Procedure

### Step 1: Download Docker

1. Visit the official Docker website: https://www.docker.com
2. Download Docker Desktop suitable for your operating system (Windows or macOS).

### Step 2: Install Docker

1. Launch the downloaded installer.
2. Follow the installation wizard instructions.
3. For Windows users, enable WSL 2 if prompted during installation.

### Step 3: Start Docker

1. Open Docker Desktop.
2. Wait until Docker Engine starts successfully.

### Step 4: Verify Installation

Open Command Prompt or Terminal and execute:

```bash
docker --version
```

This command displays the installed Docker version.

### Step 5: Run a Test Container

Execute the following command:

```bash
docker run hello-world
```

Docker downloads the Hello World image and runs it in a container to confirm that Docker is functioning correctly.

### Step 6: Download an Image

Pull the Nginx web server image using:

```bash
docker pull nginx
```

### Step 7: Launch a Container

Run the Nginx container with:

```bash
docker run -d -p 8080:80 nginx
```

Open a browser and navigate to:

```
http://localhost:8080
```

The Nginx welcome page should appear.

### Step 8: View Running Containers

To display active containers, use:

```bash
docker ps
```

### Step 9: Stop a Container

Terminate a running container with:

```bash
docker stop <container_id>
```

Replace `<container_id>` with the actual container ID.

## Purpose of Docker

Docker provides a standardized environment for application development, deployment, and execution. By packaging applications together with all required dependencies, Docker eliminates compatibility issues that often occur when moving applications between different systems.

The platform improves development efficiency, supports scalability, and simplifies application deployment. Docker also plays a significant role in DevOps practices by enabling automation, continuous integration, continuous delivery, and microservices-based architectures. Since containers are lightweight compared to virtual machines, they make more efficient use of computing resources.

## Conclusion

This practical exercise involved the successful installation and verification of Docker. Various Docker commands were executed to pull images, create containers, monitor running containers, and manage container operations. The experiment highlighted Docker's ability to simplify application deployment while maintaining consistency across multiple environments. Due to its lightweight architecture, portability, and scalability, Docker has become an important tool for modern software development and DevOps workflows.