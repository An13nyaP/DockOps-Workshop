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

