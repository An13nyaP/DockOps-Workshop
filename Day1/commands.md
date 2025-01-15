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
---

## 15. **Dockerfile: Building Your Own Docker Images**

### What is a Dockerfile?
A **Dockerfile** is a script-like text file containing instructions to automate the process of building a Docker image. It specifies:
- The base image to use.
- Dependencies to install.
- Files to copy into the container.
- Commands to run inside the container.

### Structure of a Dockerfile:
Here's the general structure of a Dockerfile:

1. **Base Image**: Specify a starting point for your image.
   ```dockerfile
   FROM <base_image>
   ```

2. **Maintainer (Optional)**: Add metadata about the creator.
   ```dockerfile
   LABEL maintainer="your_email@example.com"
   ```

3. **Environment Variables (Optional)**: Define default variables.
   ```dockerfile
   ENV APP_ENV=production
   ```

4. **Working Directory**: Set the directory inside the container.
   ```dockerfile
   WORKDIR /app
   ```

5. **Copy Files**: Copy files from your system to the container.
   ```dockerfile
   COPY <source> <destination>
   ```

6. **Run Commands**: Execute commands during the image build process.
   ```dockerfile
   RUN <command>
   ```

7. **Expose Ports**: Define ports to be accessible.
   ```dockerfile
   EXPOSE <port_number>
   ```

8. **Command to Run**: Specify the default command to execute when the container starts.
   ```dockerfile
   CMD ["executable", "arg1", "arg2"]
   ```

---

### Example 1: "Hello from DockOps"

#### 1. **Dockerfile**
```dockerfile
# Use the official Python base image
FROM python:3.9-slim

# Add metadata
LABEL maintainer="dockops@example.com"

# Set working directory
WORKDIR /app

# Copy the Python script to the working directory
COPY hello.py .

# Command to run the Python script
CMD ["python", "hello.py"]
```

#### 2. **hello.py**
```python
print("Hello from DockOps!")
```

#### 3. **Build and Run**
- Build the image:
  ```bash
  docker build -t hello-dockops .
  ```
- Run the container:
  ```bash
  docker run hello-dockops
  ```
- Expected Output:
  ```plaintext
  Hello from DockOps!
  ```

---

### Example 2: A Simple Calculator

#### 1. **Dockerfile**
```dockerfile
# Use the official Python base image
FROM python:3.9-slim

# Add metadata
LABEL maintainer="dockops@example.com"

# Set working directory
WORKDIR /app

# Copy the calculator script to the working directory
COPY calculator.py .

# Install any required Python packages (if needed)
RUN pip install --no-cache-dir numpy

# Command to run the calculator script
CMD ["python", "calculator.py"]
```

#### 2. **calculator.py**
```python
def calculator():
    print("Welcome to the Simple Calculator!")
    while True:
        try:
            operation = input("Choose operation (+, -, *, / or 'q' to quit): ").strip()
            if operation.lower() == 'q':
                print("Goodbye!")
                break
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
            if operation == '+':
                print(f"Result: {num1 + num2}")
            elif operation == '-':
                print(f"Result: {num1 - num2}")
            elif operation == '*':
                print(f"Result: {num1 * num2}")
            elif operation == '/':
                if num2 != 0:
                    print(f"Result: {num1 / num2}")
                else:
                    print("Error: Division by zero!")
            else:
                print("Invalid operation!")
        except ValueError:
            print("Invalid input! Please enter numeric values.")

if __name__ == "__main__":
    calculator()
```

#### 3. **Build and Run**
- Build the image:
  ```bash
  docker build -t simple-calculator .
  ```
- Run the container:
  ```bash
  docker run -it simple-calculator
  ```
- Expected Output:
  The calculator will prompt you for operations and numbers interactively.

## 15. **Publishing a Docker Image**

### **1. Create a Docker Hub Account**
If you don’t already have a Docker Hub account, create one at [Docker Hub](https://hub.docker.com/). 

---

### **2. Login to Docker Hub**
Log in to Docker Hub from the CLI:
```bash
docker login
```
- Enter your Docker Hub username and password when prompted.
- Successful login will display a message: `Login Succeeded`.

---

### **3. Tag the Image**
Docker Hub requires images to be tagged with the format `<username>/<repository>:<tag>`. Tag your image appropriately:
```bash
docker tag my-docker-image <your_dockerhub_username>/<repository_name>:<tag>
```

### Example:
```bash
docker tag my-docker-image ananya123/my-first-image:v1.0
```
- `my-docker-image`: The name of your locally built image.
- `ananya123`: Replace with your Docker Hub username.
- `my-first-image`: The repository name where you want to publish the image.
- `v1.0`: Tag version (optional; defaults to `latest` if omitted).

---

### **4. Push the Image**
Push the tagged image to Docker Hub:
```bash
docker push <your_dockerhub_username>/<repository_name>:<tag>
```

### Example:
```bash
docker push ananya123/my-first-image:v1.0
```

---

### **5. Verify the Published Image**
- Go to your Docker Hub profile ([Docker Hub](https://hub.docker.com/)) and check for the repository and the uploaded image.

---

### **6. Run the Published Image from Docker Hub**
You can now pull and run the image from Docker Hub on any machine:
```bash
docker pull <your_dockerhub_username>/<repository_name>:<tag>
docker run -it <your_dockerhub_username>/<repository_name>:<tag>
```

### Example:
```bash
docker pull ananya123/my-first-image:v1.0
docker run -it ananya123/my-first-image:v1.0
```

---

### Notes:
- Replace `<your_dockerhub_username>` with your actual username.
- Make sure your image works correctly before pushing it to Docker Hub.
- For private repositories, ensure your Docker Hub account or the repository allows access.

