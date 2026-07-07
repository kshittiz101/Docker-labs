# 🐳 Docker Nginx Static Website Lab

## 📋 Overview

A simple Docker lab demonstrating how to containerize a static website using Nginx Alpine.

---

## 📁 Project Structure

```
lab1/
├── Dockerfile
├── index.html
└── README.md
```

---

## 🔧 Dockerfile

```dockerfile
# Use lightweight Alpine Linux version of Nginx (only ~5MB)
FROM nginx:alpine

# Set maintainer label (good for documentation)
LABEL maintainer="your-email@example.com"
LABEL description="Static website with Nginx"

# Remove default nginx welcome page (optional, keeps things clean)
RUN rm -rf /usr/share/nginx/html/*

# Copy custom HTML file to nginx web root
COPY index.html /usr/share/nginx/html/

# Expose port 80 (documentation purposes)
EXPOSE 80

# Nginx will start automatically (CMD is inherited from base image)
# The base nginx image already has: CMD ["nginx", "-g", "daemon off;"]
```

---

## 🚀 Build & Run

### 1. Build Image

```bash
docker build -t travel-ui .
```

> **What it does:** Builds a Docker image tagged as `travel-ui` using the Dockerfile and build context from the current directory (`.`)

### 2. Run Container

```bash
docker run -d -p 8000:80 --name travel travel-ui:latest
```

> **What it does:** Runs a container named `travel` in detached mode (background) from the `travel-ui:latest` image, mapping port 8000 on your host to port 80 inside the container.

### 3. Test

```bash
curl http://localhost:8000
# Or open browser: http://localhost:8000
```

---

## 📝 Useful Commands

| Command                     | Description                 |
| --------------------------- | --------------------------- |
| `docker ps`                 | List running containers     |
| `docker logs travel`        | View container logs         |
| `docker exec -it travel sh` | Open shell inside container |
| `docker stop travel`        | Stop container              |
| `docker rm -f travel`       | Remove container            |
| `docker rmi travel-ui`      | Remove image                |

---

## 🧹 Cleanup

```bash
docker rm -f travel
docker rmi travel-ui
```

---

## 📚 Resources

- [Docker Documentation](https://docs.docker.com/)
- [Nginx Docker Image](https://hub.docker.com/_/nginx)

---

**Happy Containerization! 🐳**
