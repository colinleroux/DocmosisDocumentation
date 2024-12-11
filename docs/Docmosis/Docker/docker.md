# Docker


Create a new or amend current docker file on host. To run ...

`docker build --tag customdocmosis/tornado -f mydockerfile.txt .`

---

Use docker-compose
create a Dockerfile and add to directory - then:

create a docker-compose.yaml
```
version: '3.3'

services:
  tornado:
    build:
      context: /home/colin/
    ports:
      - "8080:8080"
    volumes:
      - /home/colin/docmosisTemplates:/home/docmosis/templates
    environment:
      DOCMOSIS_KEY: "XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      DOCMOSIS_SITE: "Free Trial Tornado"
      DOCMOSIS_ADMINPW: "password"

```
then  :

`$sudo docker-compose up --build`

---

### 1. **Check Docker Version and Info**
- **Version**: Check the Docker version installed:
  ```bash
  docker --version
  ```
- **Info**: Get system-wide information about Docker, including containers, images, and resources:
  ```bash
  docker info
  ```

---

### 2. **Explore Docker Commands**
Use the `docker help` command to see all available commands:
```bash
docker help
```

For detailed help about a specific command, use:
```bash
docker <command> --help
```

---

### 3. **Container Management Commands**
- **List Containers**:
  - Running containers:
    ```bash
    docker ps
    ```
  - All containers (including stopped ones):
    ```bash
    docker ps -a
    ```

- **Start/Stop/Restart a Container**:
  ```bash
  docker start <container_id_or_name>
  docker stop <container_id_or_name>
  docker restart <container_id_or_name>
  ```

- **Remove a Container**:
  ```bash
  docker rm <container_id_or_name>
  ```

- **View Logs of a Container**:
  ```bash
  docker logs <container_id_or_name>
  ```

- **Attach to a Running Container**:
  ```bash
  docker attach <container_id_or_name>
  ```

- **Run a Command in a Running Container**:
  ```bash
  docker exec -it <container_id_or_name> <command>
  ```
  Example: Open a bash shell inside the container:
  ```bash
  docker exec -it <container_id_or_name> bash
  ```

---

### 4. **Image Management Commands**
- **List Images**:
  ```bash
  docker images
  ```

- **Remove an Image**:
  ```bash
  docker rmi <image_id_or_name>
  ```

- **Pull an Image from Docker Hub**:
  ```bash
  docker pull <image_name>
  ```

- **Build an Image from a Dockerfile**:
  ```bash
  docker build -t <image_name> <path_to_dockerfile>
  ```

---

### 5. **Network Management Commands**
- **List Networks**:
  ```bash
  docker network ls
  ```

- **Inspect a Network**:
  ```bash
  docker network inspect <network_name>
  ```

- **Create a Network**:
  ```bash
  docker network create <network_name>
  ```

- **Connect/Disconnect a Container to/from a Network**:
  ```bash
  docker network connect <network_name> <container_id_or_name>
  docker network disconnect <network_name> <container_id_or_name>
  ```

---

### 6. **Volume Management Commands**
- **List Volumes**:
  ```bash
  docker volume ls
  ```

- **Create a Volume**:
  ```bash
  docker volume create <volume_name>
  ```

- **Inspect a Volume**:
  ```bash
  docker volume inspect <volume_name>
  ```

- **Remove a Volume**:
  ```bash
  docker volume rm <volume_name>
  ```

---

### 7. **Monitoring and Debugging**
- **Show Resource Usage of Containers**:
  ```bash
  docker stats
  ```

- **Inspect a Container’s Configuration**:
  ```bash
  docker inspect <container_id_or_name>
  ```

- **Check Docker Logs**:
  ```bash
  sudo journalctl -u docker
  ```

---

### 8. **Clean Up Resources**
- **Remove Unused Data**:
  ```bash
  docker system prune
  ```
  Add `-a` to remove unused images, not just dangling ones:
  ```bash
  docker system prune -a
  ```

- **Remove All Stopped Containers**:
  ```bash
  docker container prune
  ```

- **Remove All Unused Volumes**:
  ```bash
  docker volume prune
  ```

---

### 9. **Interactive Tools**
If you want an easier way to manage Docker:
- Install **`docker-compose`** for managing multi-container setups:
  ```bash
  sudo apt install docker-compose
  ```

- Install **`ctop`** to visualize running containers:
  ```bash
  sudo apt install ctop
  ```

---
