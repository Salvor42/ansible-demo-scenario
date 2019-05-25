FROM jenkins/jenkins:lts

USER root

# Docker integration
# ==================
RUN apt update && \
    apt -y install apt-transport-https ca-certificates gnupg2 wget && \
    wget -qO - https://download.docker.com/linux/debian/gpg | apt-key add -

RUN echo "deb https://download.docker.com/linux/debian stretch stable" \
    >/etc/apt/sources.list.d/docker-ce.list

RUN apt update && apt -y install docker-ce-cli

RUN  wget https://github.com/docker/compose/releases/download/1.23.2/docker-compose-Linux-x86_64 -O /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose


# Ansible integration
# ===================
# Add backports
RUN echo "deb http://ftp.debian.org/debian stretch-backports main" \
    >/etc/apt/sources.list.d/backports.list

RUN apt update && apt -y install -t stretch-backports ansible


USER jenkins


RUN /usr/local/bin/install-plugins.sh \
    greenballs \
    ansicolor \
    ansible \
    git \
    matrix-auth \
    ssh \
    workflow-aggregator

ENV JENKINS_USER admin
ENV JENKINS_PASS admin
 
# Skip the initial setup wizard
ENV JAVA_OPTS \
    -Djenkins.install.runSetupWizard=false \
    -Djenkins.CLI.disabled=true

#COPY config.groovy /usr/share/jenkins/ref/init.groovy.d
