FROM centos:centos7.2.1511

ENV container=docker

RUN yum install -y epel-release sudo \

  # fix locale
  && localedef --force -i en_US -f UTF-8 en_US.UTF-8 \

  # install ssh
  && yum install -y openssh-server which openssh-clients \
  && echo 'root:root123' | chpasswd \
  && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
  && systemctl enable sshd \

  # fix for systemd
  && yum install -y initscripts \

  # fix for getty consume 100% cpu
  && systemctl disable getty@tty1.service \

  && rm -rf /var/lib/yum/* \
  && yum clean all

ENTRYPOINT ["/usr/sbin/init"]
