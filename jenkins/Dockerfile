FROM jenkins/jenkins:lts-jdk21

USER root

RUN apt-get update && \
    apt-get install -y lsb-release curl gnupg

RUN curl -fsSL https://download.docker.com/linux/debian/gpg \
 | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

RUN echo \
 "deb [arch=$(dpkg --print-architecture) \
 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
 https://download.docker.com/linux/debian \
 $(lsb_release -cs) stable" \
 > /etc/apt/sources.list.d/docker.list

RUN apt-get update && apt-get install -y docker-ce-cli

# tạo docker group giống host
RUN groupadd -g 999 docker || true

# add jenkins vào docker group
RUN usermod -aG docker jenkins

USER jenkins