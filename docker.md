### Dockerfile

A **Dockerfile** is a text file that contains a series of instructions used to build a Docker image. These instructions define the base image, the environment setup, application dependencies, and the final steps to run the application. Each instruction in a Dockerfile creates a layer in the image, making it modular and reusable.

#### Basic Structure of a Dockerfile:

Here's a detailed breakdown of common Dockerfile instructions with an example:

```Dockerfile
# Use an official base image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the local directory contents into the container
COPY . /app

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose a port for the application
EXPOSE 80

# Define environment variables
ENV NAME World

# Set the default command to run when starting the container
CMD ["python", "app.py"]
```

##### Explanation of Each Instruction:

1. **FROM:**
   ```Dockerfile
   FROM python:3.8-slim
   ```
   - Specifies the base image to use for the Docker image. Here, it's a lightweight Python 3.8 image. `FROM` is usually the first instruction in a Dockerfile.

2. **WORKDIR:**
   ```Dockerfile
   WORKDIR /app
   ```
   - Sets the working directory inside the container. All subsequent instructions will be executed in this directory.

3. **COPY:**
   ```Dockerfile
   COPY . /app
   ```
   - Copies files and directories from the host filesystem into the container. In this case, it copies the current directory (`.`) to `/app` inside the container.

4. **RUN:**
   ```Dockerfile
   RUN pip install --no-cache-dir -r requirements.txt
   ```
   - Executes a command in the container at build time. Here, it installs Python dependencies listed in `requirements.txt`. `--no-cache-dir` prevents caching to reduce image size.

5. **EXPOSE:**
   ```Dockerfile
   EXPOSE 80
   ```
   - Informs Docker that the container will listen on the specified network port at runtime. This does not actually publish the port; it’s a form of documentation.

6. **ENV:**
   ```Dockerfile
   ENV NAME World
   ```
   - Sets environment variables in the container, which can be accessed by the application or subsequent instructions.

7. **CMD:**
   ```Dockerfile
   CMD ["python", "app.py"]
   ```
   - Specifies the default command to run when the container starts. It should be used to run the main program of the container.

Other common Dockerfile instructions include `LABEL`, `ARG`, `ENTRYPOINT`, `ADD`, and many more, each serving different purposes.

### Important Docker Commands

Here are some of the most important Docker commands you'll need for day-to-day Docker usage:

#### **Image Management:**

1. **Build Image:**
   ```bash
   docker build -t myapp:1.0 .
   ```
   - `-t myapp:1.0`: Tags the image with the name `myapp` and version `1.0`.
   - `.`: Specifies the build context, usually the directory containing the Dockerfile.

2. **List Images:**
   ```bash
   docker images
   ```
   - Lists all images available on the local Docker host.

3. **Remove Image:**
   ```bash
   docker rmi image_id
   ```
   - Removes an image using its ID. You can list images and get their IDs using `docker images`.

#### **Container Management:**

1. **Run a Container:**
   ```bash
   docker run -d -p 80:80 --name mycontainer myapp:1.0
   ```
   - `-d`: Runs the container in detached mode (in the background).
   - `-p 80:80`: Maps port 80 on the host to port 80 in the container.
   - `--name mycontainer`: Names the container `mycontainer`.
   - `myapp:1.0`: Specifies the image and tag to use for creating the container.

2. **List Running Containers:**
   ```bash
   docker ps
   ```
   - Lists all running containers.

3. **List All Containers (including stopped ones):**
   ```bash
   docker ps -a
   ```
   - Lists all containers, including those that are stopped.

4. **Stop a Container:**
   ```bash
   docker stop container_id
   ```
   - Stops a running container using its container ID.

5. **Remove a Container:**
   ```bash
   docker rm container_id
   ```
   - Removes a stopped container using its container ID.

6. **View Logs:**
   ```bash
   docker logs container_id
   ```
   - Displays the logs from a specific container.

7. **Execute Command in Running Container:**
   ```bash
   docker exec -it container_id bash
   ```
   - Opens an interactive terminal session in a running container. Replace `bash` with the command you need to run if not a shell.

#### **Network and Volume Management:**

1. **Create Network:**
   ```bash
   docker network create mynetwork
   ```
   - Creates a new Docker network named `mynetwork`.

2. **List Networks:**
   ```bash
   docker network ls
   ```
   - Lists all Docker networks.

3. **Create Volume:**
   ```bash
   docker volume create myvolume
   ```
   - Creates a Docker volume named `myvolume`.

4. **List Volumes:**
   ```bash
   docker volume ls
   ```
   - Lists all Docker volumes.
5. **Docker Prune:**
    ```bash
    docker system prune
    ```
    - It’s a command used to remove all stopped containers, unused networks, build caches, and dangling images. Prune is one of the most useful commands in Docker.
### Diff between docker RUN and CMD

- Use **`RUN`** for commands that need to modify the image at build time.
- Use **`CMD`** to define the default command and arguments that will run when the container starts.
- Combine **`ENTRYPOINT` and `CMD`** for more flexible and controlled runtime behaviors.

### Summary

- **Dockerfile:** A scripted file containing instructions to build a Docker image.
  - Common instructions: `FROM`, `WORKDIR`, `COPY`, `RUN`, `EXPOSE`, `ENV`, `CMD`.
  
- **Docker Commands:** Essential commands to manage Docker images, containers, networks, and volumes.
  - Image management: `docker build`, `docker images`, `docker rmi`.
  - Container management: `docker run`, `docker ps`, `docker stop`, `docker rm`, `docker logs`, `docker exec`.
  - Network and volume management: `docker network create`, `docker network ls`, `docker volume create`, `docker volume ls`.

Mastering Docker will significantly enhance your ability to develop, deploy, and manage applications consistently across various environments.
