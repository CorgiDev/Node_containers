ARG BASE_REGISTRY=registry.access.redhat.com
ARG BASE_IMAGE=ubi8/ubi
ARG BASE_TAG=8.1

FROM ${BASE_REGISTRY}/${BASE_IMAGE}:${BASE_TAG}

LABEL name="Node" \
      maintainer="Beth Gray <corgidev@outlook.com>" \
      vendor="OpenJS Foundation" \
      version="12.16.1" \
      release="12" \
      summary="Node Container Image" \
      description="This NodeJS image intended to act as a base for building and running NodeJS applications."

ARG NODE_RELEASE=12
ARG INSTALL_PKGS="nodejs npm nodejs-nodemon nss_wrapper"

WORKDIR /opt

RUN set -ex && \
    yum update -y --nogpgcheck && \
    yum -y module enable nodejs:$NODE_RELEASE && \
    yum remove -y $INSTALL_PKGS && \
    yum install -y --nogpgcheck --setopt=tsflags=nodocs $INSTALL_PKGS && \
    yum -y clean all && \
    node --version && \
    npm --version && \
    npx -v && \
    echo /opt/node_modules/.bin/:/opt/.npm-global/bin/:$PATH && \
    echo CtrlAltDelBurstAction=none >> /etc/systemd/system.conf

COPY LICENSE /licenses/nodejs

EXPOSE 8080

CMD ["node"]

HEALTHCHECK --timeout=30s CMD which node || exit 1s