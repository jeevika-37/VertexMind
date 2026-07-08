# Dockerized Application Deployment on AWS EC2

## Project Overview

This project demonstrates the deployment of a Dockerized web application on an AWS EC2 instance. The application was containerized using Docker and deployed on an Ubuntu EC2 server. The application is accessible through **port 8000** using the EC2 public IP address.

**Application URL:**

```
http://13.207.189.21:8000
```

---

# Project Objectives

- Containerize the application using Docker.
- Deploy the container on an AWS EC2 instance.
- Monitor application status and resource usage.
- Capture and inspect application logs.
- Document the deployment architecture.

---

# Technologies Used

- Docker
- AWS EC2 (Ubuntu)
- Linux
- Python HTTP Server
- Docker CLI

---

# Project Architecture

```
                    +----------------------+
                    |      End Users       |
                    +----------+-----------+
                               |
                               |
                     HTTP (Port 8000)
                               |
                  +------------v------------+
                  |      AWS EC2 Instance   |
                  |    Ubuntu Linux Server  |
                  +------------+------------+
                               |
                        Docker Engine
                               |
                  +------------v------------+
                  |      Docker Container   |
                  |-------------------------|
                  |  Python Web Application |
                  +------------+------------+
                               |
                     Docker Monitoring
                     & Docker Logging
```

---

# Docker Containerization

The application was containerized using Docker and built into an image named:

```
rps:latest
```

The container runs a Python HTTP server on port **8000**.

---

# Deployment on AWS EC2

## 1. Launch EC2 Instance

- AWS EC2 Ubuntu Instance
- Docker installed on Ubuntu

## 2. Start Docker Container

```bash
sudo docker start 5480811f9779
```

Docker Output:

```text
5480811f9779
```

---

## 3. Verify Running Container

Command

```bash
sudo docker ps
```

Output

```text
CONTAINER ID   IMAGE        STATUS        PORTS
5480811f9779   rps:latest   Up 5 minutes  0.0.0.0:8000->8000/tcp
```

---

## 4. Access Application

Open the application in a browser.

```
http://13.207.189.21:8000
```

---

# Monitoring

Basic monitoring was performed using Docker commands.

## Check Running Containers

```bash
sudo docker ps
```

Example Output

```text
CONTAINER ID   IMAGE
5480811f9779   rps:latest
```

---

## Check All Containers

```bash
sudo docker ps -a
```

Example Output

```text
CONTAINER ID   IMAGE        STATUS
5480811f9779   rps:latest   Up 5 minutes
de96c86f5d75   nginx        Exited (0)
```

---

## Monitor Resource Usage

Docker provides real-time resource monitoring using:

```bash
docker stats
```

This command displays:

- CPU Usage
- Memory Usage
- Network I/O
- Block I/O
- Running Processes

---

# Logging

Application logs were monitored using Docker's built-in logging mechanism.

## View Logs

```bash
sudo docker logs 5480811f9779
```

## Follow Logs in Real Time

```bash
sudo docker logs -f 5480811f9779
```

---

# Sample Log Output

```text
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...

157.50.15.189 - - [08/Jul/2026 05:10:16] "GET / HTTP/1.1" 200 -
157.50.15.189 - - [08/Jul/2026 05:10:16] "GET /index.css HTTP/1.1" 200 -
157.50.15.189 - - [08/Jul/2026 05:10:16] "GET /index.js HTTP/1.1" 200 -
157.50.15.189 - - [08/Jul/2026 05:10:17] "GET /Paper.png HTTP/1.1" 200 -

223.236.96.46 - - [08/Jul/2026 14:13:16] "GET / HTTP/1.1" 200 -
223.236.96.46 - - [08/Jul/2026 14:13:16] "GET /index.css HTTP/1.1" 200 -
223.236.96.46 - - [08/Jul/2026 14:13:17] "GET /logo.jpg HTTP/1.1" 200 -

147.185.132.48 - - [08/Jul/2026 14:14:30] "GET / HTTP/1.1" 200 -
```

The logs confirm that:

- The application started successfully.
- Static resources were served correctly.
- HTTP requests were successfully processed.
- Docker logs were used for monitoring application behavior and troubleshooting.

---

# Infrastructure Diagram

```
                        Internet
                            |
                            |
                  Public IP: 13.207.189.21
                            |
                     Port 8000 (HTTP)
                            |
                +--------------------------+
                |      AWS EC2 Instance    |
                |       Ubuntu Server      |
                +------------+-------------+
                             |
                      Docker Engine
                             |
                +------------v-------------+
                |      rps:latest          |
                |    Docker Container      |
                |--------------------------|
                | Python HTTP Application  |
                +------------+-------------+
                             |
                  Docker Built-in Logging
                  (docker logs / docker logs -f)
```

---

# Verification Steps

## Verify Container

```bash
sudo docker ps
```

---

## Verify Logs

```bash
sudo docker logs 5480811f9779
```

---

## Follow Live Logs

```bash
sudo docker logs -f 5480811f9779
```

---

## Verify Application

Visit:

```
http://13.207.189.21:8000
```

If the application loads successfully, the deployment is verified.

---

# Project Deliverables

| Task | Status |
|------|--------|
| Docker Containerization | ✅ Completed |
| AWS EC2 Deployment | ✅ Completed |
| Application Running on Port 8000 | ✅ Completed |
| Docker Container Monitoring | ✅ Completed |
| Docker Log Monitoring | ✅ Completed |
| Infrastructure Documentation | ✅ Completed |

---

# Future Enhancements

- Configure Docker Compose for multi-container deployment.
- Deploy behind an Nginx reverse proxy.
- Enable HTTPS using SSL certificates.
- Integrate Amazon CloudWatch for centralized monitoring.
- Use Prometheus and Grafana for advanced metrics visualization.
- Automate deployment using GitHub Actions CI/CD.

---

# Conclusion

The project successfully demonstrates containerizing a web application with Docker and deploying it on an AWS EC2 instance. The application is accessible via **http://13.207.189.21:8000**. Docker commands such as `docker ps`, `docker ps -a`, and `docker logs` were used to monitor container health and inspect application logs, providing a simple yet effective deployment and monitoring workflow suitable for cloud-based applications.
