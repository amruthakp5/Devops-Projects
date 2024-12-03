# CI/CD Pipeline for Application Deployment

## Project Overview
This project demonstrates the integration of a CI/CD pipeline for a Spring Boot application using Jenkins and Docker. The pipeline automates the following tasks:
1. Cloning the repository from GitHub.
2. Building the Spring Boot application using Jenkins.
3. Building and pushing a Docker image to DockerHub.
4. Placeholder for deploying the application (can be extended for deployment automation).

---

## Technologies Used
- **Spring Boot**: For building the web application.
- **Maven**: For dependency management and building the project.
- **Docker**: For containerizing the application.
- **Jenkins**: For automating the CI/CD pipeline.
- **GitHub**: For version control and repository management.
- **DockerHub**: For hosting the built Docker image.

---

## Prerequisites
1. **Jenkins**:
   - A Jenkins server running with necessary plugins: Git, Docker, and Maven.
   - Jenkins is configured to pull code from GitHub and run the pipeline.
   
2. **Docker**:
   - Docker is installed and running on the Jenkins server.
   - DockerHub account is required to push the built image to DockerHub.

3. **GitHub Repository**:
   - Code hosted in the GitHub repository.

4. **Java 17+**:
   - Jenkins must be installed with Java 17 or later.

---

