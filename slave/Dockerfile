FROM openjdk:8-jdk

ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000
ARG JENKINS_AGENT_HOME=/home/${user}

ENV JENKINS_AGENT_HOME ${JENKINS_AGENT_HOME}

COPY ssh_keys/id_rsa.pub /home/.ssh/

RUN groupadd -g ${gid} ${group} \
    && useradd -d "${JENKINS_AGENT_HOME}" -u "${uid}" -g "${gid}" -m -s /bin/bash "${user}" && \
    mkdir -p "${JENKINS_AGENT_HOME}/.ssh" && \
    cat /home/.ssh/id_rsa.pub > "${JENKINS_AGENT_HOME}/.ssh/authorized_keys" && \
    chown -Rf "${uid}:${gid}" "${JENKINS_AGENT_HOME}/.ssh" && \
    chmod 0700 -R "${JENKINS_AGENT_HOME}/.ssh"

# setup SSH server
RUN apt-get update \
    && apt-get install --no-install-recommends -y openssh-server \
    && rm -rf /var/lib/apt/lists/*
RUN sed -i /etc/ssh/sshd_config \
        -e 's/#PermitRootLogin.*/PermitRootLogin no/' \
        -e 's/#RSAAuthentication.*/RSAAuthentication yes/'  \
        -e 's/#PasswordAuthentication.*/PasswordAuthentication no/' \
        -e 's/#SyslogFacility.*/SyslogFacility AUTH/' \
        -e 's/#LogLevel.*/LogLevel INFO/' && \
    mkdir /var/run/sshd && \
    ln -s /usr/local/openjdk-8/bin/java /usr/bin/java

VOLUME "${JENKINS_AGENT_HOME}" "/tmp" "/run" "/var/run"
WORKDIR "${JENKINS_AGENT_HOME}"

COPY slave/setup-sshd /usr/local/bin/setup-sshd

EXPOSE 22

ENTRYPOINT ["setup-sshd"]