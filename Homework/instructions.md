# Homework: Create and Publish a Docker Image on Docker Hub

Follow these detailed instructions to create your own Docker image and publish it on Docker Hub. This exercise will help you solidify your understanding of Docker basics and demonstrate the full workflow from development to deployment.

---

## Step 1: Prerequisites

Before you begin, ensure you have the following:

1. **Docker Installed**: Docker Desktop should be installed on your system. You can download it from [Docker's official site](https://www.docker.com/products/docker-desktop/).
2. **Docker Hub Account**: If you don't have an account, sign up at [Docker Hub](https://hub.docker.com/).

---

## Step 2: Create a Project Directory

1. Open your terminal (Command Prompt, PowerShell, or any terminal you prefer).
2. Create a directory for your project:
   ```bash
   mkdir my-docker-project
   cd my-docker-project
   ```

---

## Step 3: Create a Dockerfile

1. Inside the project directory, create a file named `Dockerfile`:
   ```bash
   touch Dockerfile
   ```

2. Open the `Dockerfile` in a text editor and add the following content:
   ```dockerfile
   # Use the official Nginx image as the base image
   FROM nginx:latest

   # Copy an HTML file into the container
   COPY index.html /usr/share/nginx/html/index.html

   # Expose port 80 for web traffic
   EXPOSE 80
   ```

---

## Step 4: Create an HTML File

1. In the same directory, create a file named `index.html`:
   ```bash
   touch index.html
   ```

2. Open `index.html` and add the following content:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My First Docker Image</title>
   </head>
   <body>
       <h1>Welcome to My Docker Container!</h1>
       <p>This is a simple HTML page served by Nginx.</p>
   </body>
   </html>
   ```

---

## Step 5: Build Your Docker Image

1. Build the Docker image using the `docker build` command:
   ```bash
   docker build -t my-first-docker-image .
   ```
   
   - `-t` assigns a name to your image (here, `my-first-docker-image`).
   - The `.` specifies the current directory as the context.

2. Verify that your image was built successfully:
   ```bash
   docker images
   ```
   You should see your image listed.

---

## Step 6: Test Your Image Locally

1. Run a container from your image:
   ```bash
   docker run -d -p 8080:80 my-first-docker-image
   ```
   
   - `-d` runs the container in detached mode.
   - `-p 8080:80` maps port 8080 on your machine to port 80 in the container.

2. Open a web browser and navigate to `http://localhost:8080`. You should see your HTML page.

3. Stop the container after testing:
   ```bash
   docker ps
   docker stop <container_id>
   ```

---

## Step 7: Tag Your Image for Docker Hub

1. Log in to Docker Hub:
   ```bash
   docker login
   ```
   Enter your Docker Hub username and password.

2. Tag your image with your Docker Hub username:
   ```bash
   docker tag my-first-docker-image <your_dockerhub_username>/my-first-docker-image
   ```
   Replace `<your_dockerhub_username>` with your actual Docker Hub username.

---

## Step 8: Push Your Image to Docker Hub

1. Push your tagged image to Docker Hub:
   ```bash
   docker push <your_dockerhub_username>/my-first-docker-image
   ```

2. Verify that your image is now available on Docker Hub by visiting your repository page.

---

## Step 9: Share Your Docker Hub Repository

1. Copy the URL of your Docker Hub repository.
2. Share the URL to showcase your work.

---

## Bonus: Clean Up

1. Remove the container:
   ```bash
   docker rm <container_id>
   ```
2. Remove the image locally (optional):
   ```bash
   docker rmi my-first-docker-image
   ```

---

## Congratulations!
You’ve successfully created and published a Docker image to Docker Hub. This process demonstrates the fundamental steps of working with Docker and preparing images for distribution.

