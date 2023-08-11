FROM alpine:3.11
MAINTAINER Nguyen Thai Ha (thaiha@gmail.com)
ARG PACKER_VERSION="1.7.6"
ARG TERRAFORM_VERSION="1.0.8"
#ARG ANSIBLE_VERSION="2.8.12"
RUN apk update && apk upgrade
RUN apk add ca-certificates && update-ca-certificates
RUN apk add --no-cache --update \
        curl \
        unzip \
        docker-py \
        bash \
        python3 \
        libffi-dev \
        python3-dev \
        py3-netaddr \
        jq \
        openssh-client \
        gettext \
        git \
        make \
        openssl-dev \        
        sshpass \
        openssh-client \
        tzdata
RUN if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi && \
    echo "**** install pip ****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade pip setuptools wheel requests jmespath && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi

# Install Ansible
RUN echo "===> Installing Ansible..." && \
    #pip install ansible==${ANSIBLE_VERSION}
    apk add --no-cache --update ansible

RUN ansible-galaxy collection install ansible.netcommon --ignore-errors && \
    ansible-galaxy collection install cisco.ios --ignore-errors

RUN echo "===> VMware vCenter with Ansible..." && \
    pip install pyvmomi && pip install dnspython


# install packer and terraform
RUN curl https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip -o packer_${PACKER_VERSION}_linux_amd64.zip && unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /usr/local/bin && rm packer_${PACKER_VERSION}_linux_amd64.zip
RUN curl https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -o terraform_${TERRAFORM_VERSION}_linux_amd64.zip && unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/local/bin && rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN mkdir -p /opt/workspace

# Clean up
RUN rm -rf /var/cache/apk/* && pip cache purge && rm -f packer_${PACKER_VERSION}_linux_amd64.zip && rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip

WORKDIR /opt/workspace
