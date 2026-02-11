🐳 Docker Deep Dive – Complete Guide
📌 Overview

This document provides a deep understanding of Docker, including:

The problem Docker solves

Virtual Machines vs Containers

Docker Architecture

Dockerfile Deep Dive

Key Docker Commands

Docker Networking

Volumes & Data Persistence

Docker Compose

1️⃣ The Problem Docker Solves

Before Docker, developers faced major issues:

❌ Problems:

“It works on my machine” problem

Different OS environments (Windows, Linux, Mac)

Dependency conflicts

Difficult application deployment

Heavy Virtual Machines consuming large resources

✅ How Docker Solves This:

Packages application + dependencies together

Runs consistently across environments

Lightweight compared to VMs

Faster startup time

Simplifies CI/CD pipelines

Docker ensures:

Build once → Run anywhere

2️⃣ Virtual Machines vs Docker
Feature	Virtual Machine	Docker (Containers)
OS	Each VM has its own OS	Shares host OS
Size	GBs	MBs
Boot Time	Minutes	Seconds
Performance	Heavy	Lightweight
Resource Usage	High	Low
Isolation	Strong	Process-level
Architecture Comparison

VM Architecture:
Hardware → Host OS → Hypervisor → Guest OS → App

Docker Architecture:
Hardware → Host OS → Docker Engine → Containers → App

👉 Containers are faster and more efficient.

3️⃣ Understanding Docker Architecture

When Docker is installed, the following components are installed:

🔹 Docker Engine

Docker Engine consists of:

1. Docker Client

Command line interface (docker build, docker run)

Sends commands to Docker daemon

2. Docker Daemon (dockerd)

Runs in background

Builds images

Runs containers

Manages networks & volumes

3. Docker REST API

Communication between client and daemon

🔹 Docker Objects

Images

Containers

Networks

Volumes

Registries (Docker Hub)

4️⃣ Dockerfile Deep Dive

A Dockerfile is a script that contains instructions to build a Docker image.

Example Dockerfile:
# Base Image
FROM node:18

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY . .

# Expose port
EXPOSE 3000

# Start application
CMD ["npm", "start"]

🔍 Explanation of Each Instruction
🔹 FROM

Defines base image

Every Dockerfile must start with FROM

🔹 WORKDIR

Sets working directory inside container

🔹 COPY

Copies files from local system to container

🔹 RUN

Executes commands during image build

🔹 EXPOSE

Documents which port the container listens on

🔹 CMD

Default command executed when container starts

5️⃣ Key Docker Commands
🔹 Image Commands
docker build -t myapp .
docker images
docker rmi image_id

🔹 Container Commands
docker run -d -p 3000:3000 myapp
docker ps
docker ps -a
docker stop container_id
docker rm container_id

🔹 Logs & Exec
docker logs container_id
docker exec -it container_id bash

6️⃣ Docker Networking

Docker provides built-in networking.

🔹 Types of Networks
1️⃣ Bridge (default)

Used for standalone containers

Internal private network

2️⃣ Host

Shares host network

No isolation

3️⃣ None

No network access

4️⃣ Custom Bridge

Allows container-to-container communication

Example:

docker network create mynetwork
docker run --network mynetwork myapp

7️⃣ Volumes & Persistence

By default, container data is temporary.

If container is deleted → data is lost.

🔹 Docker Volume

Volumes store data outside container.

Create Volume:
docker volume create myvolume

Run Container with Volume:
docker run -v myvolume:/data myapp


Now data persists even if container is removed.

8️⃣ Docker Compose

Docker Compose is used to run multi-container applications.

Instead of running multiple docker run commands, we use one file.

🔹 docker-compose.yml Example
version: "3.8"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root

🔹 Commands
docker-compose up
docker-compose up -d
docker-compose down


Compose helps manage:

App container

Database container

Networks

Volumes

All in one file.

🎯 Conclusion

Docker:

Solves environment inconsistency

Improves deployment speed

Uses lightweight containers

Supports networking & volumes

Enables multi-container apps using Compose

Docker is essential for:

DevOps

CI/CD

Microservices

Cloud deployments
