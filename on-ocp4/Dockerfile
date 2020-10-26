FROM registry.access.redhat.com/openshift3/jenkins-agent-maven-35-rhel7

LABEL maintainer "nishipy"

ENV EPEL_URL https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
ENV CHROME_URL https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
USER root

COPY ./etc-pki-entitlement /etc/pki/entitlement

RUN yum install -y ${EPEL_URL} \
    && yum-config-manager --enable rhel-7-server-rpms \
    && yum-config-manager --enable rhel-7-server-extras-rpms \
    && yum-config-manager --enable rhel-7-server-optional-rpms \
    && yum install -y skopeo chromedriver ipa-pgothic-fonts.noarch python-pip \
    && yum install -y  ${CHROME_URL} \
    && rm -rf /var/tmp/* 
RUN pip install selenium

USER 1001