FROM ubuntu:16.04

# Set the locale
RUN locale-gen en_US.UTF-8  

ENV DEBIAN_FRONTEND=noninteractive \
    LANGUAGE=en_US.en \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    SALT_VERSION=2016.3.2

RUN echo 'APT::Install-Recommends "0"; \n\
          APT::Get::Assume-Yes "true"; \n\
          APT::Install-Suggests "0";' > /etc/apt/apt.conf \
  && apt-get update \
  && apt-get install -y vim-nox curl \
  && curl -L https://repo.saltstack.com/apt/ubuntu/16.04/amd64/archive/${SALT_VERSION}/SALTSTACK-GPG-KEY.pub | apt-key add - \
  && echo "deb http://repo.saltstack.com/apt/ubuntu/16.04/amd64/archive/${SALT_VERSION} xenial main" > /etc/apt/sources.list.d/saltstack.list \
  && apt-get update \
  && apt-get install -y sudo software-properties-common openssh-client \
  && apt-get install -y salt-ssh=${SALT_VERSION}* salt-master=${SALT_VERSION}* \

  # cleanup
  && rm -rf /var/lib/apt/lists/* \
  && apt-get -y autoremove \
  && apt-get clean

ENTRYPOINT ["/bin/true"]

