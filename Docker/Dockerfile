# Copyright 2018-2023 Istituto Nazionale di Fisica Nucleare
# SPDX-License-Identifier: EUPL-1.2

FROM centos:7

# Allow customization of nginx user ID and name
ARG USERNAME=testngx
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

# install dependencies
COPY provide-deps.sh /tmp/
COPY provide-user.sh /tmp/
COPY nginx.repo /etc/yum.repos.d/nginx.repo
    
RUN yum update -y && \
    sh /tmp/provide-deps.sh && \
    sh /tmp/provide-user.sh ${USERNAME} ${USER_UID} ${USER_GID} && \
    yum -y install nginx nginx-module-njs && \
    yum clean all && rm -rf /var/cache/yum

EXPOSE 80 8080
STOPSIGNAL SIGQUIT

# docker run -it -p 80:80 -v $PWD:/tmp nginx-seminar bash