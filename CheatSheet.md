# Detailed Docker Cheat Sheet

This cheat sheet provides detailed Docker commands, descriptions, and use cases.

---

## Docker Installation and Version

### Check Docker Installation
```bash
docker --version
```
- Displays the installed Docker version.

### Verify Docker is Running
```bash
docker info
```
- Shows system-wide information about Docker, including running containers, images, and configurations.

---

## Docker Images

### Build an Image
```bash
docker build -t "image-name:tag" .
```
- **`-t`**: Tags the image with `image-name:tag` (e.g., `myapp:v1`).
- **`.`**: Specifies the build context (current directory).

### List All Images
```bash
docker images
```
- Shows all available images on your system.

### Remove an Image
```bash
docker rmi "image-id"
```
- Removes the specified image by ID or name.

### Pull an Image from Docker Hub
```bash
docker pull "repository-name[:tag]"
```
- Downloads an image from Docker Hub (e.g., `nginx:latest`).

### Tag an Image
```bash
docker tag "source-image" "target-image:tag"
```
- Creates a new tag for an existing image.

### Save and Load Images
Save an image to a file:
```bash
docker save -o "image.tar" "image-name"
```
Load an image from a file:
```bash
docker load -i "image.tar"
```

---

## Docker Containers

### Run a Container
```bash
docker run -it --name "container-name" "image-name"
```
- **`-it`**: Runs in interactive mode with a pseudo-TTY.
- **`--name`**: Assigns a name to the container.

### Run in Detached Mode
```bash
docker run -d --name "container-name" "image-name"
```
- **`-d`**: Runs the container in the background.

### Run with Port Mapping
```bash
docker run -p 8080:80 "image-name"
```
- Maps port 80 in the container to port 8080 on the host.

### Run with Volume Mounting
```bash
docker run -v "$(pwd)/data:/app/data" "image-name"
```
- Mounts the `data` directory from the host to `/app/data` in the container.

### Run with Environment Variables
```bash
docker run -e "ENV_VAR=value" "image-name"
```
- Passes an environment variable to the container.

### Run with Resource Limiting
```bash
docker run --cpus="2" --memory="1g" "image-name"
```
- Limits CPU cores to 2 and memory to 1 GB.

### Run with Restart Policy
```bash
docker run --restart always -d "image-name"
```
- Restarts the container automatically if it stops.

### Start/Stop Containers
Start a container:
```bash
docker start "container-name"
```
Stop a container:
```bash
docker stop "container-name"
```

### Restart a Container
```bash
docker restart "container-name"
```

### List Containers
Running containers:
```bash
docker ps
```
All containers:
```bash
docker ps -a
```

### Remove a Container
```bash
docker rm "container-id"
```
- Removes a stopped container.

---

## Inspecting and Debugging

### View Logs
```bash
docker logs "container-name"
```

### Follow Logs in Real Time
```bash
docker logs -f "container-name"
```

### Inspect Container Details
```bash
docker inspect "container-name"
```
- Outputs JSON with detailed configuration and state information.

### Access a Running Container
```bash
docker exec -it "container-name" bash
```
- Opens a shell inside the running container.

---

## Docker Volumes

### Create a Volume
```bash
docker volume create "volume-name"
```

### List Volumes
```bash
docker volume ls
```

### Inspect a Volume
```bash
docker volume inspect "volume-name"
```

### Remove a Volume
```bash
docker volume rm "volume-name"
```

---

## Docker Networks

### List Networks
```bash
docker network ls
```

### Create a Network
```bash
docker network create "network-name"
```

### Connect a Container to a Network
```bash
docker network connect "network-name" "container-name"
```

### Disconnect a Container from a Network
```bash
docker network disconnect "network-name" "container-name"
```

---

## Cleanup and Maintenance

### Remove All Stopped Containers
```bash
docker container prune
```

### Remove All Unused Images
```bash
docker image prune
```

### Remove All Unused Data (Images, Containers, Networks)
```bash
docker system prune -a
```
- **`-a`**: Removes all unused images, not just dangling ones.

---

## Docker Compose

### Start Services
```bash
docker-compose up
```
- Starts services defined in `docker-compose.yml`.

### Start Services in Detached Mode
```bash
docker-compose up -d
```

### Stop Services
```bash
docker-compose down
```

### View Logs
```bash
docker-compose logs
```

### Scale Services
```bash
docker-compose up --scale "service-name"=3
```
- Scales the specified service to 3 instances.

---

## Advanced Features

### Build Multi-Stage Docker Images
```dockerfile
FROM node:16 AS builder
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
```

### Multi-Container Networking
- Link services in `docker-compose.yml` for seamless communication.

---

This cheat sheet is a comprehensive guide for managing Docker images, containers, networks, and volumes.
