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
RUN pip install ansible
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ansible.tgz /etc
RUN cd /etc/; tar -xzvf ansible.tgz; rm ansible.tgz

#RUN ssh-keygen -q -t rsa -N '' -f /root/.ssh/id_rsa
COPY ssh_key_anisblemaster.tgz /root/.ssh
RUN cd /root/.ssh/; tar -xzvf ssh_key_anisblemaster.tgz; rm ssh_key_anisblemaster.tgz
#RUN cat /tmp/key_debserver >> /root/.ssh/authorized_keys

ENV TERM xterm
#CMD ["bash"]
CMD ["/usr/bin/supervisord", "-n"]
