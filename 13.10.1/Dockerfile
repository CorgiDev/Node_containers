ARG BASE_REGISTRY=registry.access.redhat.com
ARG BASE_IMAGE=ubi8/ubi
ARG BASE_TAG=8.1

FROM ${BASE_REGISTRY}/${BASE_IMAGE}:${BASE_TAG}

LABEL name="Node" \
      maintainer="Beth Gray <corgidev@outlook.com>" \
      vendor="OpenJS Foundation" \
      version="13.11.1" \
      release="13" \
      summary="Node Container Image" \
      description="This NodeJS image is intended for building and running NodeJS applications."

ARG NODE_VERSION=13.11.1
ARG NODE_TARBALL=node-v${NODE_VERSION}.tar.gz
ARG NODE_SHA256=a47e0a2ce346c7d5b25a5d4cb3c9efa82068a2a32a2885332d7d354f9e120706
ARG COMPILE_DWNLD_PKGS="python3 gcc-c++ wget make"
ARG POST_INSTALL_PKGS="nodejs-nodemon nss_wrapper"

COPY LICENSE /licenses/nodejs

WORKDIR /opt

# Need to add in a sha256 check
RUN set -ex && \
    yum update -y --nogpgcheck && \
    yum -y clean all && \
    yum remove -y $INSTALL_PKGS && \
    yum install --nogpgcheck -y python2 gcc-c++ wget make && \
    wget https://nodejs.org/dist/v${NODE_VERSION}/${NODE_TARBALL} -O /opt/${NODE_TARBALL} && \
    tar -zxf ./${NODE_TARBALL} && rm -fv ./${NODE_TARBALL} && \
    cd node-v${NODE_VERSION} && \
    ./configure && \
    make -j4 && \
    make install && \
    cd .. && \
    rm -Rf node-v${NODE_VERSION} && \
    rm -Rf ${NODE_TARBALL} && \
    rm -rfv /opt/* /var/cache/yum && \
    yum install -nogpgcheck nodejs-nodemon nss_wrapper --setopt=tsflags=nodocs -y && \
    npm update && \
    yum clean all && \
    node --version && \
    npm --version && \
    npx -v && \
    echo /opt/node_modules/.bin/:/opt/.npm-global/bin/:$PATH && \
    echo CtrlAltDelBurstAction=none >> /etc/systemd/system.conf

EXPOSE 8080

CMD ["node"]