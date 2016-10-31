FROM ubuntu:16.04

ENV SALT_VERSION=2016.3.2

RUN apt-get update \
  && apt-get install -y vim-nox curl \
  && curl -L https://repo.saltstack.com/apt/ubuntu/14.04/amd64/archive/${SALT_VERSION}/SALTSTACK-GPG-KEY.pub | apt-key add - \
  && echo "deb http://repo.saltstack.com/apt/ubuntu/14.04/amd64/archive/${SALT_VERSION} trusty main" > /etc/apt/sources.list.d/saltstack.list \
  && apt-get update \
  && apt-get install -y sudo software-properties-common openssh-client \
  && apt-get install -y salt-ssh=${SALT_VERSION}* \

  # cleanup
  && rm -rf /var/lib/apt/lists/* \
  && apt-get -y autoremove \
  && apt-get clean

ENTRYPOINT ["/bin/true"]

