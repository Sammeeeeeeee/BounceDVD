# BounceDVD

A minimal, secure, and lightweight Docker container that serves a webpage displaying the classic bouncing DVD logo screensaver. On click, it hits a corner.

<img src="https://img.shields.io/badge/GPL--3.0-red?style=for-the-badge" /> <img src="https://img.shields.io/badge/Docker%20Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white" /> 
<img alt="GitHub commit activity" src="https://img.shields.io/github/commit-activity/t/Sammeeeeeeee/BounceDVD"> <img alt="GitHub Release Date" src="https://img.shields.io/github/release-date/Sammeeeeeeee/BounceDVD"> <img alt="Docker Image Version" src="https://img.shields.io/docker/v/Sammeeeeeeee/BounceDVD"> <img alt="GitHub Actions Workflow Status" src="https://img.shields.io/github/actions/workflow/status/Sammeeeeeeee/BounceDVD/build-publish.yml">

This project has no practical application, I made it to practice applying secure container design and best DevSecOps practices.

## Usage
### Build from source
1. Clone the repo
2. ```bash
	git clone https://github.com/Sammeeeeeeee/BounceDVD.git
	cd BounceDVD
	docker-compose up -d --build
	```
3. Visit `http://localhost:8080`
### Use docker registry

1. ```bash
	docker run -p 8080:80 sammeeeeeeee/dvd-bounce:latest
	```
2. Visit `http://localhost:8080`


##  Security & Best Practices

-   **Scratch-Based Image:**  
    Uses `FROM scratch` to remove all OS bloat, to reduce attack surface.
    
-   **Minimal User Privileges:**  
    Runs as a dedicated non-root user (`dvdapp`, UID 65532). Zero trust based file permissions.
    
-   **Immutable Filesystem:**  
    Uses `read_only: true`, makes static files read-only and directories non-writable wherever possible.
    
-   **Dropped Capabilities:**  
    Drops all Linux capabilities except `NET_BIND_SERVICE` (for binding to port 80 without root).
    
-   **Hardened Caddyfile:**  
    Adds HTTP security headers (CSP, HSTS, X-Frame-Options, etc.). Caddy's admin endpoint disabled.
    
-   **No Privilege Escalation:**  
    `security_opt: no-new-privileges:true` so no processes can gain more rights.
    
-   **Isolated Network:**  
    Runs in a bridged Docker network with inter-container communication disabled.
    
-   **Build Sanitation:**  
    Dockerfile removes non-needed tools (`apk`, shell scripts, backups, temp files). Config files are made immutable.
    
-   **CI Pipeline Security:**  
    GitHub Actions hardened with `step-security/harden-runner`. Docker image scanned with Trivy. Critical vuln count logged.


## Health & Observability

-   `/health` endpoint.
    
-   `HEALTHCHECK` baked into Dockerfile.
    
-   Logs discarded to reduce surface.

## Technologies:

-   **HTML5 & JavaScript** – Frontend animation logic with `<canvas>`, runs client-side only'
    
-   **Caddy (v2)** – Lightweight static file server.
    
-   **Docker & Docker Compose** – Containerized deployment with tightly scoped config.
    
-   **GitHub Actions** – CI/CD pipeline for building, scanning, and publishing the image.
    
-   **Trivy** – Vulnerability scanner integrated in CI.
    
-   **Alpine Linux** – Minimal base image for reduced surface and size'

-   **step-security/harden-runner** – Prevents unexpected outbound network calls in CI.