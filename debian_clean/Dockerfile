FROM debian:jessie
MAINTAINER Michael Hoffmann

ENV DEBIAN_FRONTEND noninteractive 
RUN apt-get update && \
    apt-get install -y \
      net-tools \
      apt-utils \
      openssh-server \
      ca-certificates \
      bash \
      bash-completion \
      ncurses-base \
      vim \
      tree \
      gettext \
      curl \
      wget \
      logrotate \
      supervisor \
      less \
      git \
      subversion \
      default-jdk \
      apt-transport-https \
      python.yaml \
      python-dev \
      python-pip \
      python-crypto \
      python-jinja2 \
      python-httplib2 \
      python-keyczar \
      python-paramiko \
      python-setuptools \
      python-apt \
      procps && \
    apt-get clean

RUN mkdir -p /var/run/sshd /var/log/supervisor
RUN mkdir /root/.ssh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN ssh-keygen -q -t rsa -N '' -f /root/.ssh/id_rsa
COPY id_rsa_host.pub /tmp/
COPY id_rsa_ansible.pub /tmp/
RUN cat /tmp/id_rsa_host.pub >> /root/.ssh/authorized_keys; rm /tmp/id_rsa_host.pub
RUN cat /tmp/id_rsa_ansible.pub >> /root/.ssh/authorized_keys; rm /tmp/id_rsa_ansible.pub

ENV TERM xterm
#CMD ["bash"]
CMD ["/usr/bin/supervisord", "-n"]
