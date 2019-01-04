FROM alpine:3.7
MAINTAINER ha nguyen <thaiha@gmail.com>
ARG packer_version="1.2.4"
RUN apk update
RUN apk upgrade
RUN apk add ca-certificates && update-ca-certificates
RUN apk add --no-cache --update \
        curl \
        unzip \
        bash \
        python \
        py-pip \
        openssh \
        git \
        make \
        build-base \
        openssl-dev \
        perl \
        tzdata
RUN pip install --upgrade pip
RUN pip install awscli
RUN curl https://releases.hashicorp.com/packer/${packer_version}/packer_${packer_version}_linux_amd64.zip -o packer_${packer_version}_linux_amd64.zip
RUN unzip packer_${packer_version}_linux_amd64.zip -d /usr/local/bin
RUN mkdir -p /opt/workspace
RUN rm /var/cache/apk/*
WORKDIR /opt/workspace
CMD packer version
