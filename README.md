# CI/CD pipeline setup using Github, Jenkins and Docker.

This is a simple static app that i will deploy using aws ec2 instance.

## Prerequisites

Before you begin, make sure you have the following installed on your aws ec2 instance:

- Docker
- Jenkins
- Git 

## Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```

2. Navigate to the project directory:

   ```bash
   cd your-repo-name
   ```
3. Install JRE on you machine using the following command:

   ```bash
   sudo apt install default-jre
   ```
4. After Installing JRE check if java is installed or not.

   ```bash
   java --version
   ```
5. Now Install Jenkins with the following commands:
 
 ```bash
 sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
   ```
  
6. After Installing Jenkins, you should also install docker using the following command:

   ```bash
   sudo apt install docker.io
   ```
7. Build the image from the docker file.

   ```bash
   sudo docker build -t oxer-app:lts .
   ```
8. Check for the docker images:

   ```bash
   sudo docker images
   ```
9. Use the following command so you dont have to use sudo all the time when running docker commands:

   ```bash
   sudo chown ubuntu /var/run/docker.sock
   ```
10. If you get the permission denied error while building the job in jenkins use following command and then restart the jenkins server:

```bash
   sudo usermod -aG docker jenkins
   newgrp docker
   ```
11. Now create a Jenkins job and configure it with the github repo.

12. Choose the option Execute shell and add following commands in it:

```bash
   docker rm -f "container_name"
   docker run -f -p 32768:80 --name <container_name> <image_name>
   ```
13. To automatically trigger the jenkins job whenever there is a change in the repository enable the webhook option from the jenkin's job configuration.

14. Also add webhook in your github repository.
