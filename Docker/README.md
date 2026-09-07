# Docker

## 1. Brief Introduction

Docker is a containerization platform used to package applications and their dependencies into portable images and run them as isolated containers.

Docker gives DevOps teams a repeatable unit for build, test and deployment. The same versioned image can move from a developer workstation through CI/CD and into a test or production environment.

### Key Concepts

- **Image** — Read-only package containing application code, dependencies and metadata.
- **Container** — Running instance of an image.
- **Dockerfile** — Instructions used to build an image.
- **Registry** — Repository used to store and distribute images.
- **Volume** — Persistent storage that can outlive a container.
- **Network** — Connectivity layer between containers and external systems.

---

## 2. Docker Architecture

Docker Engine consists of a long-running daemon, an API and the Docker CLI. The CLI sends requests to the daemon. The daemon creates and manages Docker objects including images, containers, networks and volumes.

| Component | Role |
|---|---|
| Docker CLI | User-facing command-line client that sends requests to Docker Engine |
| dockerd | Long-running daemon that manages Docker objects |
| Docker API | Interface used by the CLI and applications to control the daemon |
| Image | Template from which containers are created |
| Container | Runtime instance of an image |
| Registry | Stores and distributes images |
| Volumes / Networks | Provide persistent data and connectivity |

---

## 3. Key Commands

| Command | Purpose | Example |
|---|---|---|
| `docker version` | Show client/server versions | `docker version` |
| `docker pull` | Download an image | `docker pull nginx:latest` |
| `docker build` | Build an image | `docker build -t myapp:1.0 .` |
| `docker run` | Create and start a container | `docker run -d -p 8080:80 nginx` |
| `docker ps` | List running containers | `docker ps` |
| `docker ps -a` | List all containers | `docker ps -a` |
| `docker logs` | Read container logs | `docker logs -f myapp` |
| `docker exec` | Run a command inside a container | `docker exec -it myapp sh` |
| `docker stop` | Stop a container | `docker stop myapp` |
| `docker rm` | Remove a container | `docker rm myapp` |
| `docker images` | List local images | `docker images` |
| `docker push` | Push an image to a registry | `docker push registry.example/myapp:1.0` |
| `docker compose up` | Start a Compose application | `docker compose up -d` |

---

## 4. Real-Time Project Usage

A typical DevOps workflow using Docker:

1. Create a Dockerfile for the application.
2. Build the image in CI and give it an immutable release/commit tag.
3. Run the same image locally or in a test environment.
4. Scan the image for known vulnerabilities.
5. Push the approved image to a private registry.
6. Deploy that image to Docker Compose, a VM or Kubernetes.

This provides consistency between development, testing and deployment environments.

---

## 5. Practical Example

### Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "app.py"]
```

### Build the Image

```bash
docker build -t university-app:1.0 .
```

### Run the Container

```bash
docker run -d --name university-app -p 8000:8000 university-app:1.0
```

### View Logs

```bash
docker logs -f university-app
```

For production, credentials should not be stored in Dockerfiles or image layers. Runtime secrets or a dedicated secret-management solution should be used.

---

## 6. Alternatives & Comparison

| Technology | Strength | When to Consider |
|---|---|---|
| Docker | Mature developer workflow and broad ecosystem | General container build/run workflows and local development |
| Podman | Daemonless and strong rootless workflow | Linux environments preferring daemonless/rootless containers |
| containerd | Core container runtime used by many platforms | Lower-level runtime integration, especially with Kubernetes |
| Buildah | Container image building without a Docker daemon | Linux-focused image build automation |

---

## 7. Best Practices & Troubleshooting

- Use small base images and multi-stage builds where appropriate.
- Pin important base/dependency versions.
- Never store passwords or private keys in Dockerfiles.
- Use `.dockerignore` to reduce build context.
- Use meaningful release tags.
- Check `docker logs`, `docker inspect` and exit codes during failures.
- Monitor image size, vulnerabilities and unused resources.

---

## 8. Suggested Internship Mini-Project

Containerize a small Flask or Node.js application.

The project should:

1. Add a health endpoint.
2. Build the Docker image in CI.
3. Scan the image for vulnerabilities.
4. Push the image to a registry.
5. Deploy the exact same image to a test environment.
6. Document the Dockerfile, image tags and troubleshooting process.

---

## Conclusion

Docker is a foundational DevOps skill because it connects development, CI/CD, registries and deployment.

Important areas to learn include:

- Image lifecycle
- Container runtime behavior
- Networking
- Storage
- Secure image delivery

---

## References

- Docker Engine Documentation https://docs.docker.com/engine/
- Docker CLI Documentation  https://docs.docker.com/reference/cli/docker/
- Docker Reference  https://docs.docker.com/reference/
