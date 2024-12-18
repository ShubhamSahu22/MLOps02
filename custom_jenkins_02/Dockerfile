# Use a Jenkins image as base image
FROM jenkins/jenkins:lts

# Install Docker
USER root
RUN apt-get update -y && apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release && \
    install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg \
    -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list && \
    apt-get update -y && apt-get install -y \
    docker-ce \
    docker-ce-cli \
    containerd.io && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Configure Docker to run as a non-root user
RUN usermod -aG docker jenkins

# Enable DinD
RUN mkdir -p /var/lib/docker
VOLUME /var/lib/docker
