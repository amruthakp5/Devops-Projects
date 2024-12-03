# CI/CD Pipeline for Application Deployment

## Project Overview
This project demonstrates the integration of a CI/CD pipeline for a Spring Boot application using Jenkins and Docker. The pipeline automates the following tasks:
1. Cloning the repository from GitHub.
2. Building the Spring Boot application using Maven.
3. Automating CI/CD pipeline using Jenkins
4. Building and pushing a Docker image to DockerHub.

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
  
## Pipeline Stages
The pipeline consists of the following stages:

### 1. **Clone Repository**
   - Clones the source code from the GitHub repository to the Jenkins workspace.

### 2. **Build Application**
   - Uses Maven to compile and package the Spring Boot application into a `.jar` file.

### 3. **Docker Build**
   - Builds a Docker image using the `Dockerfile` and tags it with the repository name and `:latest`.

### 4. **Docker Push**
   - Pushes the Docker image to DockerHub for deployment or sharing.


---
## Step 1: Setup Jenkins Server on AWS EC2 Instance
### 1. **Setup a Linux(Ubuntu/Amazon Linux) EC2 Instance**
   - Log in to the Amazon management console, open EC2 Dashboard, click on the Launch Instance drop-down list, and click on Launch Instance.
   - Once the Launch an instance window opens, provide the name of your EC2 Instance
   - Choose an Instance Type. Here you can select the type of machine, number of vCPUs, and memory that you want to have. Select t2.micro which is free-tier eligible.
   - Create new key pair.
   - Now under Network Settings, Choose the default VPC with Auto-assign public IP in enable mode. Create a new Security Group, provide a name for your security group, allow ssh traffic, and custom default TCP port of 8080 which is used by Jenkins and 8082 for spring boot application.
   - Rest of the settings we will keep them at default and go ahead and click on Launch Instance.
   - Now connect to instance using PuTTY.
### 2. **Installing Packages**
     sudo apt update && sudo apt upgrade -y
     sudo apt install openjdk-17-jdk –y
     sudo apt install maven –y
     sudo apt install git –y
     sudo apt install docker.io -y

     sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \ https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
     echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \https://pkg.jenkins.io/debian-stable binary/ | sudo tee \ /etc/apt/sources.list.d/jenkins.list > /dev/null
     sudo apt-get update
     sudo apt-get install Jenkins
     systemctl start Jenkins
     systemctl status Jenkins

   _Now let’s try to access the Jenkins server through our browser. For that take the public IP of your EC2 instance and paste it into your favorite browser with 8080 port._
   
   _To unlock Jenkins we need to go to the path /var/lib/jenkins/secrets/initialAdminPassword and fetch the admin password to proceed further._
   
   _Now on the Customize Jenkins page, we can go ahead and install the suggested plugins._
   
   _Now we can create our first Admin user, provide all the required data and proceed to save and continue._
   _Now we are ready to use our Jenkins Server._

## Step 2: Integrate GitHub with Jenkins
* Install Git on Jenkins Instance
* Install Github Plugin on Jenkins GUI
* Configure Git on Jenkins GUI

   _To install the GitHub plugin lets go to our Jenkins Dashboard and click on manage Jenkins_
  
   _On the next page, click on manage plugins_
  
   _Now in order to install any plugin we need to select Available Plugins, search for Github Integration, select the plugin, and finally click on `Install without restart`_
  
   _Now let’s configure Git on Jenkins. Go to Manage Jenkins, and click on Global Tool Configuration._
  
   _Under `Git installations`, provide the name Git, and under `Path`, we can either provide the complete path where our Git is installed on the Jenkins machine or just put any name, in my case I put Git to allow Jenkins to automatically search for Git. Then click on Save to complete the installation._

## Step 3: Run the Application
* Clone the Repository on the EC2 instance:

        git clone <git_repo_url>
        cd <proect_folder>
* Build the Application using Maven:

        mvn clean package
* Run the Application
  
        java –jar target/springbootapp-0.0.1-SNAPSHOT.jar
* Let’s try to access the Application server through our browser. For that take the public IP of your EC2 instance and paste it into your favorite browser with 8082 port

## Step 4: Setup Docker
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo usermod -aG docker Jenkins
     docker build -t my-app:latest .
     docker images
     docker run -p 8082:8082 my-app:latest

## Step 5: Integrate Docker with Jenkins
   _To install the GitHub plugin lets go to our Jenkins Dashboard and click on manage Jenkins_
  
   _On the next page, click on manage plugins_
  
   _Now in order to install any plugin we need to select Available Plugins, search for Github Integration, select the plugin, and finally click on `Install without restart`_

   _Now let’s configure Docker on Jenkins._
   
       Go to Manage Jenkins → Manage Credentials → Add your DockerHub username and password as credentials.
       Use an ID like dockerhub_credentials.


## Step 5: Create a Jenkins Pipeline Job
 In Jenkins Webserver:
 1.	Click New Item in Jenkins.
 2.	Select Pipeline and name your job (e.g., SpringBoot-CI-CD).
 3.	Under the Pipeline section:
       -	Choose Pipeline script from SCM.
       - Select Git as the SCM.
       -	Enter your repository URL.
       -	Provide credentials if the repository is private.
       -	Specify the branch (e.g., main or master).
       -	Set the Script Path to Jenkinsfile.

4.  Save the Jenkins pipeline configuration
5.  Click Build Now to start the pipeline.

 

     

   





     








