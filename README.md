# DevOps-Example
This is a sample Spring Boot Application, used to explain the Jenkins pipeline, in creating a full CI/CD flow using docker too.

# Using Jenkins with Docker
First of all to use jenkins with docker, we will have to know that as we are running Jenkins inside a docker container, and we need access to docker to
build our services images, so first of all let's build a Jenkins image with docker installed inside it. Let's check the dockerfile to 
build this Jenkins image with docker inside, you will just have to put this file into any folder, and run the docker build command.

# Dockerfile for Jenkins
```
from jenkins/jenkins:lts
USER root
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update  -qq \
    && apt-get install docker-ce=17.12.1~ce-0~debian -y
RUN usermod -aG docker jenkins
```

Just place this Dockerfile in any folder and run the following commands:

$ docker image build -t jenkins-docker .

Now that the docker image has already been built, we can run the Jenkins in a docker container with the command:

$ docker container run -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock jenkins-docker

![image](https://github.com/user-attachments/assets/74e157ed-a3db-4ddd-9540-8ea625652051)


![image](https://github.com/user-attachments/assets/628118e9-6aca-448f-8aa9-c8e3fb03ab58)


![image](https://github.com/user-attachments/assets/89bdd740-6e95-4b5d-a345-d0fb9e749547)


