FROM ubuntu:18.04

ENV container=docker

RUN apt-get update \
  && apt-get -y upgrade \
  && apt-get install -y libdbus-1-3 libnih-dbus1 sudo software-properties-common ifupdown python vim \
# install ssh
  && apt-get install -y openssh-server \
  && echo 'root:root123' | chpasswd \
  && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
  && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
  && systemctl enable ssh \
# fix missing resolvconf
  && cd /tmp \
  && apt-get download resolvconf \
  && dpkg --unpack resolvconf_*_all.deb \
  && rm /var/lib/dpkg/info/resolvconf.postinst \
  && dpkg --configure resolvconf \
  && apt-get install -yf \
  && apt-mark hold resolvconf \
# set the locale
  && LC_ALL=C apt-get install locales \
  && locale-gen --purge en_US.UTF-8 \
# fix for getty consume 100% cpu
  && systemctl disable getty@tty1.service \
  && rm -f /lib/systemd/system/multi-user.target.wants/getty.target \
# fix for stderr: no crontab for root
  && echo '# no crontab for root yet' | crontab - \
# cleanup
  && rm -rf /var/lib/apt/lists/* \
  && apt-get autoremove \
  && apt-get clean

ENTRYPOINT ["/sbin/init"]
