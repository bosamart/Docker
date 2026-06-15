# Docker Lab — Session 01: Installation & Basics
**Environment:** EVE-NG | Ubuntu 24.04 Server | 2 vCPU | 2GB RAM

---

## VM Setup in EVE-NG

| Setting | Value |
|---------|-------|
| Image | Linux — Ubuntu 24.04 |
| CPU | 2 |
| RAM | 2048 MB |
| Node name | docker-node1 |

---

## Step 1 — First Boot Checks

```bash
# Update system packages
sudo apt update && sudo apt upgrade -y

# Check internet connectivity
ping 8.8.8.8

# Confirm Ubuntu version
cat /etc/os-release
```

---

## Step 2 — Install Docker

```bash
# Download and run Docker's official install script
curl -fsSL https://get.docker.com | sh

# Add your user to docker group (avoid typing sudo every time)
sudo usermod -aG docker $USER

# Reboot to apply group changes
sudo reboot
```

---

## Step 3 — Verify Docker Installation

```bash
# Check Docker version
docker --version

# Run test container
docker run hello-world
```

**Expected output:**
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

✅ If you see the message above — Docker is successfully installed.

---

## Step 4 — Basic Docker Commands

### Run your first real container
```bash
# Run Nginx web server in background (-d = detached)
docker run -d -p 80:80 --name mynginx nginx

# Verify it is running
docker ps

# Check logs
docker logs mynginx

# Go inside the container
docker exec -it mynginx bash

# Exit container
exit

# Stop container
docker stop mynginx

# Remove container
docker rm mynginx
```

### Essential Docker commands reference

| Command | What it does |
|---------|-------------|
| `docker ps` | Show running containers |
| `docker ps -a` | Show all containers (including stopped) |
| `docker images` | List downloaded images |
| `docker pull nginx` | Download an image |
| `docker run` | Create and start a container |
| `docker stop` | Stop a running container |
| `docker rm` | Remove a container |
| `docker rmi` | Remove an image |
| `docker logs` | View container logs |
| `docker exec -it` | Enter a running container |

---

## Step 5 — Write Your First Dockerfile

```bash
# Create a working directory
mkdir myapp && cd myapp

# Create a simple HTML page
echo "<h1>Hello from my Docker container!</h1>" > index.html

# Create the Dockerfile
nano Dockerfile
```

**Dockerfile contents:**
```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install -y nginx
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

```bash
# Build your image
docker build -t myapp:v1 .

# Run your custom image
docker run -d -p 80:80 --name myapp myapp:v1

# Test it in browser or curl
curl http://localhost
```

---

## Step 6 — Docker Compose (Multi-container)

```bash
# Install Docker Compose
sudo apt install docker-compose-plugin -y

# Create a compose file
nano docker-compose.yml
```

**docker-compose.yml contents:**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  app:
    build: .
    ports:
      - "5000:5000"
```

```bash
# Start all services
docker compose up -d

# Check status
docker compose ps

# View logs
docker compose logs

# Stop all services
docker compose down
```

---

## Key Concepts Summary

| Concept | Explanation |
|---------|-------------|
| **Image** | Blueprint/template for a container (like an ISO file) |
| **Container** | Running instance of an image |
| **Dockerfile** | Instructions to build a custom image |
| **Docker Compose** | Tool to run multiple containers together |
| **Port mapping** | `-p 80:80` = host port 80 → container port 80 |
| **Detached mode** | `-d` = runs container in background |

---

## Next Session — Preview

- Push your image to **Docker Hub**
- Set up **Docker on all 3 physical servers**
- Configure **Nginx as load balancer** across nodes
- Prepare for **k3s Kubernetes cluster** setup

---

## Troubleshooting

```bash
# Docker service not running?
sudo systemctl start docker
sudo systemctl enable docker

# Permission denied error?
# Make sure you ran usermod and rebooted
groups $USER

# Port already in use?
sudo lsof -i :80
```

---

*Lab built on physical server farm: Cisco Nexus NX-OS switch + 3 Linux nodes*
*DevOps study roadmap — targeting iBank Officer DevOps position*
