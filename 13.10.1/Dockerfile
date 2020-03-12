ARG BASE_REGISTRY=registry.access.redhat.com
ARG BASE_IMAGE=ubi8/ubi
ARG BASE_TAG=8.1

FROM ${BASE_REGISTRY}/${BASE_IMAGE}:${BASE_TAG}

LABEL name="Node" \
      maintainer="Beth Gray <corgidev@outlook.com>" \
      vendor="OpenJS Foundation" \
      version="13.10.1" \
      release="13" \
      summary="Node Container Image" \
      description="This NodeJS image is intended for building and running NodeJS applications."

ARG NODE_VERSION=13.10.1
ARG NODE_TARBALL=node-v${NODE_VERSION}.tar.gz

COPY ${NODE_TARBALL} /opt/
COPY LICENSE /licenses/nodejs

WORKDIR /opt

# Need to add in a sha256 check and the download of the tar
RUN set -ex && \
    yum update -y --nogpgcheck && \
    yum -y clean all && \
    yum install --nogpgcheck -y python3 gcc-c++ make && \
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
    yum clean all && \
    node --version && \
    npm --version && \
    npx -v && \
    echo /opt/node_modules/.bin/:/opt/.npm-global/bin/:$PATH && \
    echo CtrlAltDelBurstAction=none >> /etc/systemd/system.conf

EXPOSE 8080

CMD ["node"]

HEALTHCHECK --timeout=30s CMD which node || exit 1
