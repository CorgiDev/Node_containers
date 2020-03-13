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
      description="This NodeJS image is intended for building and running NodeJS applications."

ARG NODE_VERSION=12.16.1
ARG NODE_TARBALL=node-v${NODE_VERSION}.tar.gz
ARG NODE_SHA256=4fe8c3454f9bee5bbe72d44aa25cd931859b3037b7a9473081b3b2bd1b465b95
ARG COMPILE_DWNLD_PKGS="python2 gcc-c++ wget make"
ARG POST_INSTALL_PKGS="nodejs-nodemon nss_wrapper"


COPY LICENSE /licenses/nodejs

WORKDIR /opt

# Need to add in a sha256 check
RUN set -ex && \
    yum update -y --nogpgcheck && \
    yum remove -y $INSTALL_PKGS && \
    yum install --nogpgcheck -y ${COMPILE_DWNLD_PKGS} && \
    wget -q -O ${NODE_TARBALL} https://nodejs.org/dist/v${NODE_VERSION}/${NODE_TARBALL} && \
    echo "${NODE_SHA256} *${NODE_TARBALL}" | sha256sum -c - && \
    tar -zxf ./${NODE_TARBALL} && rm -fv ./${NODE_TARBALL} && \
    cd node-v${NODE_VERSION} && \
    ./configure && \
    make -j4 && \
    make install && \
    cd .. && \
    rm -Rf node-v${NODE_VERSION} && \
    rm -Rf ${NODE_TARBALL} && \
    rm -rfv /opt/* /var/cache/yum && \
    yum install -nogpgcheck ${POST_INSTALL_PKGS} -y && \
    npm update && \
    yum clean all && \
    node --version && \
    npm --version && \
    npx -v && \
    echo /opt/node_modules/.bin/:/opt/.npm-global/bin/:$PATH && \
    echo CtrlAltDelBurstAction=none >> /etc/systemd/system.conf

EXPOSE 8080

CMD ["node"]