FROM jenkins/jenkins:lts

COPY master/plugins.txt /usr/share/jenkins/ref/plugins.txt
COPY master/casc.yaml /var/jenkins_home/
RUN /usr/local/bin/install-plugins.sh  < /usr/share/jenkins/ref/plugins.txt

USER root
# RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
#  && apt-get update \
#  && apt-get install -y --no-install-recommends graphviz nodejs \
#  && rm -rf /var/lib/apt/lists/*
# USER jenkins