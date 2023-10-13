ARG GO_VERSION=1.20
ARG ALPINE_VERSION=3.18

FROM golang:${GO_VERSION}-alpine${ALPINE_VERSION}

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

WORKDIR /var/app

# Setup user
RUN adduser $USERNAME -s /bin/sh -D -u $USER_UID $USER_GID && \
    mkdir -p /etc/sudoers.d && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

# Install packages and Go language server
RUN apk add -q --update --no-cache \
    gpgconf \
    libgcc \
    libstdc++ \
    git \
    sudo \
    openssh-client

RUN go install -v golang.org/x/tools/gopls@latest