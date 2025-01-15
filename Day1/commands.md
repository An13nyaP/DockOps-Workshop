# Docker Commands: Step-by-Step Exploration

## 1. Checking Your Docker Installation

### Command:
```bash
docker version
```
### Purpose:
Verify that Docker is installed and check the version of the client and server.

### Example Output:
```plaintext
Client: Docker Engine - Community
 Version: 20.10.8
 API version: 1.41
 Go version: go1.16.6
Server: Docker Engine - Community
 Version: 20.10.8
 API version: 1.41 (minimum version 1.12)
```

---

## 2. Pulling and Running a Basic Ubuntu Image

### Pulling an Image:
```bash
docker pull ubuntu
```
### Purpose:
Download the latest Ubuntu image from Docker Hub to your local machine.

### Running a Container:
```bash
docker run -it ubuntu
```
### Purpose:
Start an interactive session in an Ubuntu container.

### Explanation:
- `-it`: Interactive terminal mode.
- Inside the container, you can run commands like `ls`, `pwd`, or `apt update` to explore the environment.

---

## 3. Listing Containers and Images

### Listing Running Containers:
```bash
docker ps
```
### Purpose:
See a list of containers currently running on your system.

### Listing All Containers (Running and Stopped):
```bash
docker ps -a
```

### Listing Images:
```bash
docker images
```
### Purpose:
Display all images available locally.

---

## 4. Executing Commands Inside a Container

### Command:
```bash
docker exec -it <container_id> bash
```
### Purpose:
Run commands inside a running container interactively.

### Explanation:
- `-it`: Opens an interactive terminal session.
- Replace `<container_id>` with the ID or name of the running container.

### Example:
Start an Nginx container:
```bash
docker run -d --name mynginx nginx
```
Check files inside it:
```bash
docker exec -it mynginx bash
ls /usr/share/nginx/html
```

### Detached Mode:
To keep a container running in the background:
```bash
docker run -d ubuntu
```
The container runs without tying up your terminal.

---

## 5. Exploring Data Isolation Between Containers

### Step 1: Create Two Separate Containers:
```bash
docker run -it --name container1 ubuntu
```
```bash
docker run -it --name container2 ubuntu
```

### Step 2: Create a File in Container 1:
Inside `container1`, run:
```bash
echo "Hello from Container 1" > /hello.txt
```

### Step 3: Check for the File in Container 2:
Inside `container2`, run:
```bash
ls /hello.txt
```

### Observation:
The file is not present in `container2`, demonstrating data isolation between containers.

Here's the continuation of your `commands.md` file, following the same style and structure you've provided:

```markdown
# Docker Commands: Step-by-Step Exploration

---

## 6. **Port Mapping in Docker**

### Command:
```bash
docker run -p <host_port>:<container_port> <image_name>
```
### Purpose:
Map a port from the host machine to a port inside the Docker container. This allows you to access services running inside the container from the host machine.

### Example:
```bash
docker run -p 8080:80 my-web-app
```
### Explanation:
- `8080`: Port on the host.
- `80`: Port inside the container (typically used for web services).
- `my-web-app`: The image name.

With this command, you can now access the application inside the container at `http://localhost:8080`.

---

## 7. **Environment Variables in Docker**

### Command:
```bash
docker run -e <ENV_VAR_NAME>=<value> <image_name>
```
### Purpose:
Pass environment variables into the container when it starts. These can be used by applications running inside the container.

### Example:
```bash
docker run -e DB_HOST=localhost -e DB_PORT=5432 my-app
```
### Explanation:
- `DB_HOST=localhost`: Sets the environment variable `DB_HOST` to `localhost` inside the container.
- `DB_PORT=5432`: Sets the environment variable `DB_PORT` to `5432`.

These environment variables can be accessed by the application inside the container.

---

## 8. **Viewing Environment Variables Inside a Running Container**

### Command:
```bash
docker exec <container_id> env
```
### Purpose:
View the environment variables inside a running container.

### Example:
```bash
docker exec mynginx env
```
### Explanation:
This command runs `env` inside the `mynginx` container to list all environment variables in use.

---

## 9. **Setting Default Environment Variables in Dockerfile**

### Command (in Dockerfile):
```dockerfile
ENV <ENV_VAR_NAME> <value>
```
### Purpose:
Set environment variables during the build process of the Docker image. These variables will be available to any containers that use this image.

### Example:
```dockerfile
ENV APP_ENV=production
```
### Explanation:
This sets `APP_ENV` to `production` when the Docker image is built. Any container created from this image will have the `APP_ENV` variable set to `production`.

---

## 10. **Removing Environment Variables**

### Command:
```bash
docker run --rm -e <ENV_VAR_NAME> -e <ENV_VAR_NAME2> <image_name>
```
### Purpose:
Run a container while passing environment variables but without persisting them after the container stops.

### Example:
```bash
docker run --rm -e DB_HOST=localhost -e DB_PORT=5432 my-app
```
### Explanation:
This command sets `DB_HOST` and `DB_PORT` for the running container, but these variables are discarded after the container stops (since `--rm` is used to automatically remove the container when it exits).

---

## 11. **Inspecting a Running Container's Details**

### Command:
```bash
docker inspect <container_id>
```
### Purpose:
Get detailed information about a running container, such as its network settings, mounted volumes, environment variables, and more.

### Example:
```bash
docker inspect mynginx
```
### Explanation:
This will output detailed JSON-formatted data about the `mynginx` container, including all of its settings and configurations.

---

## 12. **Removing a Container**

### Command:
```bash
docker rm <container_id>
```
### Purpose:
Remove a stopped container from the system. This does not delete the image.

### Example:
```bash
docker rm mynginx
```
### Explanation:
This removes the container `mynginx` from the system. If the container is still running, you'll need to stop it first using `docker stop`.

---

## 13. **Removing an Image**

### Command:
```bash
docker rmi <image_name>
```
### Purpose:
Remove an image from the local Docker environment.

### Example:
```bash
docker rmi my-web-app
```
### Explanation:
This command removes the image `my-web-app` from the local system. If there are containers created from this image, they must be removed first.

---

## 14. **Viewing Docker Logs for a Running Container**

### Command:
```bash
docker logs <container_id>
```
### Purpose:
View the logs generated by a container, which can be helpful for troubleshooting.

### Example:
```bash
docker logs mynginx
```
### Explanation:
This will display the logs of the `mynginx` container. You can use the `-f` flag to follow the logs in real-time.

---

## 15. **Scaling a Service with Docker Compose**

### Command:
```bash
docker-compose up --scale <service_name>=<number_of_instances>
```
### Purpose:
Scale up a service in a Docker Compose environment to run multiple instances of the same service.

### Example:
```bash
docker-compose up --scale web=3
```
### Explanation:
This command scales the `web` service to 3 instances, effectively running 3 containers of the web service in the Docker Compose setup.

---
```

