FROM registry.access.redhat.com/openshift3/jenkins-agent-maven-35-rhel7

LABEL maintainer "nishipy"

ENV EPEL_URL https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
ENV CHROME_URL https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
USER root

COPY ./etc-pki-entitlement /etc/pki/entitlement

RUN subscription-manager register --username <ID> --password <PASSWD> --auto-attach \
    && subscription-manager repos --enable=rhel-7-server-rpms \
    && subscription-manager repos --enable=rhel-7-server-extras-rpms \
    && subscription-manager repos --enable=rhel-7-server-optional-rpms
RUN yum install -y ${EPEL_URL} \
    && yum install -y skopeo chromedriver ipa-pgothic-fonts.noarch python-pip \
    && yum install -y  ${CHROME_URL} \
    && rm -rf /var/tmp/* \
    && rm -rf /etc/pki/entitlement
RUN pip install selenium
RUN subscription-manager unregister
USER 1001