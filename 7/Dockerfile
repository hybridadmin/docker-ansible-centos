FROM centos:7
LABEL maintainer="Tinashe Chikomo <tinashe@chikomo.net>"
ENV container=docker

# fix - https://githubmemory.com/repo/pypa/pip/issues/10219
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

ENV pip_packages "ansible yamllint ansible-lint pymysql"

# Install systemd -- See https://hub.docker.com/_/centos/
RUN yum -y update; yum clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

# Install requirements.
RUN yum makecache fast \
 && yum -y install deltarpm epel-release initscripts \
 && yum -y update \
 && yum -y install \
      sudo \
      curl \
      wget \
      which \
      python3 \
      python3-setuptools \
 && yum clean all

# Install Ansible via Pip.
RUN pip3 install -U pip
RUN pip3 install -U $pip_packages

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible
ADD https://raw.githubusercontent.com/hybridadmin/misc-scripts/master/linux/ansible/hosts /etc/ansible/hosts
ADD https://raw.githubusercontent.com/hybridadmin/misc-scripts/master/linux/ansible/ansible.cfg etc/ansible/ansible.cfg

VOLUME ["/sys/fs/cgroup"]
CMD ["/usr/lib/systemd/systemd"]
