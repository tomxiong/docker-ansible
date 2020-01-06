# pull base image
FROM alpine:3.9

# Labels.
LABEL maintainer="tomxiongzh@gmail.com" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.name="tomxiong/ansible" \
    org.label-schema.description="Ansible inside Docker" \
    org.label-schema.url="https://github.com/tomxiong/docker-ansible" \
    org.label-schema.vcs-url="https://github.com/tomxiong/docker-ansible" \
    org.label-schema.vendor="Tom Xiong" \
    org.label-schema.docker.cmd="docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/id_rsa tomxiong/ansible:2.9-alpine-3.9"

RUN apk --no-cache add \
        sudo \
        python \
        py-pip \
        openssl \
        ca-certificates \
        sshpass \
        openssh-client \
        rsync \
        git && \
    apk --no-cache add --virtual build-dependencies \
        python-dev \
        libffi-dev \
        openssl-dev \
        build-base && \
    pip install --upgrade pip cffi && \
    pip install ansible && \
    pip install mitogen ansible-lint && \
    pip install --upgrade pywinrm && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/*

RUN mkdir /ansible && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

WORKDIR /ansible

CMD [ "ansible-playbook", "--version" ]
