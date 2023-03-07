FROM jenkins/agent as agent
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN apt-get install curl -y
WORKDIR /usr/local
RUN curl -L https://dl.dagger.io/dagger/install.sh | VERSION=0.3.13 sh
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli