FROM ubuntu:18.04

# Install dependencies
RUN apt-get update -y 
RUN apt-get install python-dev python-pip -y
RUN pip install --upgrade pip
RUN pip install --upgrade ansible
# RUN pip install --upgrade awscli
RUN timedatectl set-timezone Asia/Saigon
RUN localectl set-locale LANG=en_US.utf8
