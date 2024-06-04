![alt text](docker-logo.png)

Docker is a tool for **containerization**. 
Hypervisors / Virtual Machines can isolate and run multiple operating systems on a single machine. But it has fixed resource allocation. That's where docker comes in.
Applications run on top of the docker engine and share the same operating system kernel. The applications running in the docker uses resources dynamically according to their needs.
Docker is actually a daemon (background process) named *dockerd* and gives us OS level virtualisation.

1. Start with a **DockerFile** which tells how to configure the environment that runs your application.
2. The Dockerfile is used to build an **Image**, which contains an OS, dependencies, code etc. We can apply these images to Docker Hub and share it to the world.
3. The docker should be run as a **container**, which is actually just isolated code. Containers are portable and stateless.

## 1. Dockerfile

A Dockerfile contains a collection of instructions.

```dockerfile
# Typically a linux distro and version
FROM debian:latest

# Source directory to put our code into.
# All next commands will be executed inside this directory
WORKDIR /usr/src

# Run any command
RUN apt-get update && \
    apt-get install -y python3 python3-pip

RUN useradd --create-home app_user

# Add a non-root user
USER app_user

# Copy the code on our local machine to the image
COPY app.py .

# To use an api_key, we set it as an environment variable
ENV API_KEY=hi_mom

# Expose a port to make it accessible from the outside
EXPOSE 8000

# Command to run when starting up a container
CMD ["python3", "-m", "http.server", "8000"]
# Alternatively, we may use an entry point allowing us to add arguments to the commands 
# ["python3", "-m", "http.server"]
# CMD ["8000"]

# OPTIONAL

# Labels for extra meta-data
LABEL version=1.0

# HEALTHCHECK to make sure the container is running properly

# Mount a volume with a persistent disk
# Used when the container will have data needed later / shared with other containers
VOLUME /db/data
```

## 2. Image

Install **Docker Desktop**, which also installs **Docker CLI**. Then, to build the image, run

    docker build .

To tag it with a recognizable name, 

    docker build . -t myContainer

Add the files that are not wanted to be included in the docker image to the **.dockerignore** file.

Open Docker desktop and view the image there. We can identify the vulnerabilities of each layer using Docker Scout.

## 3. Container

Run the container by clicking the `Run` button, or by running 

    docker run myContainer

To see all running containers, run

    docker ps

To stop a container, run

    docker container stop myContainer

To forcefully stop

    docker container kill myContainer

To remove the container

    docker container remove myContainer

`docker push` will upload the container to a remote registry.

    docker push <url>

The container can then run on a cloud like AWS using Elastic Container Service or on Serverless platforms like Google Cloud.

To download a container from the cloud, run

    docker pull <container_url>

## More

**Docker Compose** is a tool for managing multi-container application. It allows you to define multiple applications and docker images in a single `yaml` file.

    docker-compose up
    docker-compose down

In a massive scale, we might need **Orchestration tools** like **Kubernetes** to run and manage containers. It's only needed for highly complex high traffic system.
