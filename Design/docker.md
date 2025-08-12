Key Docker commands for developing, debugging, and deploying **microservices** effectively.

## ✅ Part 1: Must-Know **Docker Commands** for Microservices

### 📦 1. **Image Management**

```bash
docker build -t myapp:1.0 .       # Build image from Dockerfile
docker images                     # List all local images
docker rmi myapp:1.0              # Remove an image
docker tag myapp:1.0 myrepo/myapp:latest  # Tag image for registry
docker push myrepo/myapp:latest   # Push to Docker Hub/ECR
docker pull nginx                 # Pull image from registry
```

---

### 🏃 2. **Container Lifecycle**

```bash
docker run -d -p 8080:80 nginx    # Run container in detached mode
docker ps                         # List running containers
docker ps -a                      # List all (including stopped) containers
docker stop <container_id>        # Stop container
docker start <container_id>       # Start stopped container
docker rm <container_id>          # Remove container
docker exec -it <container_id> bash  # Exec into running container
```

---

### 🧪 3. **Debugging & Logs**

```bash
docker logs <container_id>        # View container logs
docker inspect <container_id>     # See detailed container info (network, volumes, etc.)
docker stats                      # Real-time resource usage of containers
docker diff <container_id>        # Changes made to container’s FS
```

---

### 📁 4. **Volumes & Bind Mounts**

```bash
docker volume create mydata       # Create a named volume
docker run -v mydata:/data ...    # Mount named volume
docker run -v $(pwd)/app:/app ... # Bind mount local folder
```

---

### 🔗 5. **Networking**

```bash
docker network ls                 # List networks
docker network create my-net     # Create user-defined bridge network
docker run --network my-net ...  # Attach container to that network
```

---

## ✅ Part 2: What Else to Know in Docker for Microservices

Beyond basic commands, here's what you should understand conceptually and practically for **microservice architecture**:

---

### 🏗️ 1. **Dockerfile Best Practices**

* Use slim base images (`alpine`, `openjdk:17-slim`)
* Use `.dockerignore` to exclude unnecessary files
* Minimize layers with fewer `RUN` commands
* Use multi-stage builds for smaller images

✅ Example:

```Dockerfile
FROM maven:3.9-eclipse-temurin-17 as builder
COPY . /app
WORKDIR /app
RUN mvn clean package

FROM openjdk:17-alpine
COPY --from=builder /app/target/app.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

### 🔒 2. **Security**

* Don’t run containers as root (use non-root user)
* Scan images with tools like **Trivy**, **Docker Scout**, **Snyk**
* Keep base images and dependencies up to date
* Avoid hardcoding secrets — use env vars, secrets managers

---

### 🧪 3. **Multi-Container Applications**

Use **`docker-compose`** to run services (e.g., app + DB + Redis) together for local dev.

📄 `docker-compose.yaml` example:

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db
  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: secret
```

```bash
docker-compose up -d    # Run everything
docker-compose logs     # View logs
docker-compose down     # Stop and remove containers
```

---

### 📤 4. **CI/CD Integration**

* Docker images are often built and pushed in CI pipelines using:

  * `docker build`
  * `docker tag`
  * `docker push`

You should know how to:

* Use **Docker with GitHub Actions, Jenkins, or GitLab**
* Version your microservices via image tags (`v1.0.3`, `latest`, `feature-xyz`)
* Push to **Docker Hub**, **Amazon ECR**, **Google Artifact Registry**, etc.

---

### 🧠 5. **Docker + Kubernetes**

* Docker is used to build and package services
* Kubernetes runs **containers**, not Docker per se (uses containerd or CRI-O under the hood)
* You push Docker images to a registry, and **Kubernetes pulls them** into pods

Know how to:

* Reference Docker image in Kubernetes Deployment:

```yaml
containers:
- name: myapp
  image: myrepo/myapp:1.0
```

---

## 📌 Summary Cheat Sheet

| Task                | Docker Command                |
| ------------------- | ----------------------------- |
| Build Image         | `docker build -t myapp .`     |
| Run Container       | `docker run -p 8080:80 myapp` |
| List Containers     | `docker ps`                   |
| Logs                | `docker logs <id>`            |
| Bash Into Container | `docker exec -it <id> bash`   |
| Push Image          | `docker push myrepo/myapp`    |
| Compose Up          | `docker-compose up -d`        |

---

## ✅ Optional (Advanced, But Nice to Know)

* `BuildKit` for faster builds
* `Docker context` for managing multiple environments
* `Docker Desktop Extensions` for monitoring
* Integration with **OpenTelemetry** or **Jaeger** for tracing containerized apps

