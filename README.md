# ToDo-AWS

# README: Deploy Docker Container to EC2 using Ansible
Link to WebApp:- http://16.170.232.207/
## Overview
This Ansible playbook automates the deployment of a Docker container from Docker Hub onto an EC2 instance. The playbook ensures that Docker is installed and running, pulls the specified Docker image, and runs the container with the desired configuration.

Breakdown of the Playbook (todo_deploy.yml)
---
- name: Deploy Docker container from Docker Hub to EC2 instance
  hosts: all
  become: yes
  tasks:

Task 1: Ensure Docker is Installed and Running

    - name: Ensure Docker is running
      service:
        name: docker
        state: started
        enabled: yes
        
This task ensures Docker is installed and running.

The service module:

name: docker: Refers to the Docker service.
state: started: Starts Docker if it's not running.
enabled: yes: Ensures Docker starts automatically when the machine reboots.

Task 2: Download the Application from Docker Hub

    - name: Pull the Docker image from Docker Hub
      docker_image:
        name: shakibkhatri/getting-started:latest
        source: pull
        
The docker_image module:

name: shakibkhatri/getting-started:latest: Specifies the Docker image to download.
source: pull: Tells Ansible to pull the image from Docker Hub.
What is a Docker Image? A Docker image is like a pre-configured blueprint of an application. It contains everything the application needs to run (code, dependencies, configurations, etc.).

Task 3: Run the Docker Container

    - name: Run the Docker container
      docker_container:
        name: todo-App
        image: shakibkhatri/getting-started:latest
        state: started
        ports:
          - "80:80"
        restart_policy: always
        
The docker_container module:

name: todo-App: Names the running container as todo-App.
image: shakibkhatri/getting-started:latest: Uses the Docker image pulled earlier.
state: started: Ensures the container is running.
ports: "80:80": Maps port 80 of the EC2 instance to port 80 of the container, making the application accessible via the internet.
restart_policy: always: Ensures the container restarts automatically if it crashes or the EC2 instance reboots.

What is a Docker Container? A Docker container is a running instance of a Docker image. It's like a lightweight virtual machine that runs an application independently.
