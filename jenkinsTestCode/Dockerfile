# Use the LTS version of Jenkins to ensure stability
FROM jenkins/jenkins:lts

# Switch to root user for installing dependencies
USER root

# Update package list and install dependencies including Python 3
RUN apt-get update && apt-get install -y \
    lsb-release \
    python3 \
    python3-pip \
    curl \
    ca-certificates \
    gnupg

# Add Docker repository and install Docker CLI
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg

RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

RUN apt-get update && apt-get install -y docker-ce-cli

# Switch back to Jenkins user
USER jenkins

# Install required Jenkins plugins (blueocean and docker-workflow) using the plugin CLI
RUN jenkins-plugin-cli --verbose --plugins "blueocean:1.25.3 docker-workflow:1.28"
