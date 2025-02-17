FROM jenkins/jenkins:lts-jdk17

USER root

RUN apt update && apt install -y docker.io

RUN usermod -aG docker jenkins