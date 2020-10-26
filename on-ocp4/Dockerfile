FROM registry.access.redhat.com/openshift3/jenkins-agent-maven-35-rhel7

LABEL maintainer "nishipy"

ENV EPEL_URL https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
ENV CHROME_URL https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
USER root

COPY ./etc-pki-entitlement /etc/pki/entitlement
# Copy entitlements
COPY ./etc-pki-entitlement /etc/pki/entitlement
# Copy subscription manager configurations
COPY ./rhsm-conf /etc/rhsm
COPY ./rhsm-ca /etc/rhsm/ca

# Delete /etc/rhsm-host to use entitlements from the build container
RUN rm /etc/rhsm-host && \
    # Initialize /etc/yum.repos.d/redhat.repo
    # See https://access.redhat.com/solutions/1443553
    yum repolist --disablerepo=* && \
    subscription-manager repos --enable rhel-7-server-rpms && \
    subscription-manager repos --enable rhel-7-server-extras-rpms && \
    subscription-manager repos --enable rhel-7-server-optional-rpms && \
    yum install -y ${EPEL_URL} &&\
    yum install -y skopeo chromedriver ipa-pgothic-fonts.noarch python-pip &&\
    yum install -y  ${CHROME_URL} &&\
    rm -rf /var/tmp/* &&\
    rm -rf /etc/pki/entitlement &&\ 
    pip install selenium

USER 1001