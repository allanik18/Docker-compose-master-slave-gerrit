FROM jenkins/jenkins:lts

COPY master/plugins.txt /usr/share/jenkins/ref/plugins.txt
COPY master/casc.yaml /var/jenkins_home/
RUN /usr/local/bin/install-plugins.sh  < /usr/share/jenkins/ref/plugins.txt

USER root