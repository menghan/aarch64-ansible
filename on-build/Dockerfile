# ref:https://github.com/William-Yeh/docker-ansible/blob/master/ubuntu16.04-onbuild/Dockerfile

FROM resin/aarch64-python:2.7-slim

MAINTAINER Menghan Zheng <menghan412@gmail.com>


RUN ["cross-build-start"]

RUN DEBIAN_FRONTEND=noninteractive  apt-get update && \
    \
    \
    echo "===> Installing Ansible..."  && \
    pip install ansible  && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    echo 'localhost' > /etc/ansible/hosts

RUN ["cross-build-end"]


COPY ansible-playbook-wrapper /usr/local/bin/

ONBUILD  RUN  DEBIAN_FRONTEND=noninteractive  apt-get update   && \
              echo "===> Updating TLS certificates..."         && \
              apt-get install -y openssl ca-certificates

ONBUILD  WORKDIR  /tmp
ONBUILD  COPY  .  /tmp
ONBUILD  RUN  \
              echo "===> Diagnosis: host information..."  && \
              ansible -c local -m setup all



# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]
