FROM centos:centos7.2.1511

ENV container=docker

RUN yum install -y epel-release sudo \

  # install ssh
  && yum install -y openssh-server \
  && echo 'root:root123' | chpasswd \
  && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
  && systemctl enable sshd \

  # fix for systemd
  && yum install -y initscripts \

  && rm -rf /var/lib/yum/* \
  && yum clean all

ENTRYPOINT ["/usr/sbin/init"]
