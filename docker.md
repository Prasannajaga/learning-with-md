**# Docker Commands Cheat Sheet**

## **1️⃣ Docker Version & Info**

- **Check Docker version:**
  ```sh
  docker --version
  ```
- **Get system-wide information:**
  ```sh
  docker info
  ```

## **2️⃣ Working with Images**

- **List all images:**
  ```sh
  docker images
  ```
- **Search for an image in Docker Hub:**
  ```sh
  docker search <image-name>
  ```
- **Download an image:**
  ```sh
  docker pull <image-name>
  ```
- **Remove an image:**
  ```sh
  docker rmi <image-id>
  ```
- **Remove all unused images:**
  ```sh
  docker image prune -a
  ```

## **3️⃣ Working with Containers**

- **Run a container in interactive mode:**
  ```sh
  docker run -it <image-name> /bin/bash
  ```
- **Run a container in detached mode:**
  ```sh
  docker run -d -p 8080:80 --name my-container nginx
  ```
- **List running containers:**
  ```sh
  docker ps
  ```
- **List all containers (including stopped ones):**
  ```sh
  docker ps -a
  ```
- **List only container IDs:**
  ```sh
  docker ps -q
  ```
- **Stop a running container:**
  ```sh
  docker stop <container-id>
  ```
- **Start a stopped container:**
  ```sh
  docker start <container-id>
  ```
- **Restart a container:**
  ```sh
  docker restart <container-id>
  ```
- **View container logs:**
  ```sh
  docker logs <container-id>
  ```
- **Remove a stopped container:**
  ```sh
  docker rm <container-id>
  ```
- **Remove all stopped containers:**
  ```sh
  docker container prune
  ```

## **4️⃣ Building & Managing Containers**

- **Build an image from a Dockerfile:**
  ```sh
  docker build -t my-app .
  ```
- **Save an image to a file:**
  ```sh
  docker save -o my-app.tar my-app
  ```
- **Load a saved image:**
  ```sh
  docker load -i my-app.tar
  ```

## **5️⃣ Networking in Docker**

- **List networks:**
  ```sh
  docker network ls
  ```
- **Create a network:**
  ```sh
  docker network create my-network
  ```
- **Connect a container to a network:**
  ```sh
  docker network connect my-network <container-id>
  ```
- **Remove a network:**
  ```sh
  docker network rm my-network
  ```

## **6️⃣ Docker Volumes (Data Storage)**

- **List volumes:**
  ```sh
  docker volume ls
  ```
- **Create a volume:**
  ```sh
  docker volume create my-volume
  ```
- **Attach volume to a container:**
  ```sh
  docker run -v my-volume:/app/data -it ubuntu /bin/bash
  ```
- **Remove a volume:**
  ```sh
  docker volume rm my-volume
  ```

## **7️⃣ Docker Compose**

- **Start services defined in ************************`docker-compose.yml`************************:**
  ```sh
  docker-compose up -d
  ```
- **Stop services:**
  ```sh
  docker-compose down
  ```

## **8️⃣ Quick Cleanup Commands**

- **Remove all stopped containers:**
  ```sh
  docker container prune
  ```
- **Remove all unused images:**
  ```sh
  docker image prune -a
  ```
- **Remove all unused networks:**
  ```sh
  docker network prune
  ```
- **Remove all unused volumes:**
  ```sh
  docker volume prune
  ```

### 🚀 **Now you're ready to work with Docker!**

