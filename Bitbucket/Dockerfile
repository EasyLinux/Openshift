FROM debian:buster-slim

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN apt-get update \
    && apt-get install -y --no-install-recommends tzdata curl ca-certificates fontconfig locales \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_VERSION jdk8u275-b01

RUN set -eux; \
    ARCH="$(dpkg --print-architecture)"; \
    case "${ARCH}" in \
       aarch64|arm64) \
         ESUM='e5de2bad40eb5859141d6f43c80a729089c2d69ba5dc2b698750a5d1f43f3c74'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u275-b01/OpenJDK8U-jre_aarch64_linux_hotspot_8u275b01.tar.gz'; \
         ;; \
       armhf|armv7l) \
         ESUM='2e228d39d00ba8d974fd8ccdaaee0225833e79594251b64c724485c4fc94870f'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u275-b01/OpenJDK8U-jre_arm_linux_hotspot_8u275b01.tar.gz'; \
         ;; \
       ppc64el|ppc64le) \
         ESUM='0e3200ab2a1d7e3d8ea09d89c2b5d7399ec137d2ecbd7fb5130cfa1d904c77c5'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u275-b01/OpenJDK8U-jre_ppc64le_linux_hotspot_8u275b01.tar.gz'; \
         ;; \
       s390x) \
         ESUM='ebf2775adb51863b14fe649e4d2bdd87ce3c63b3113c3f3c7223d3c4ab5ee209'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u275-b01/OpenJDK8U-jre_s390x_linux_hotspot_8u275b01.tar.gz'; \
         ;; \
       amd64|x86_64) \
         ESUM='a044da8bf198ad756b2bbb83f3d48ddeeffb934b9a9974d9b9bb6d0034413a83'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u275-b01/OpenJDK8U-jre_x64_linux_hotspot_8u275b01.tar.gz'; \
         ;; \
       *) \
         echo "Unsupported arch: ${ARCH}"; \
         exit 1; \
         ;; \
    esac; \
    curl -LfsSo /tmp/openjdk.tar.gz ${BINARY_URL}; \
    echo "${ESUM} */tmp/openjdk.tar.gz" | sha256sum -c -; \
    mkdir -p /opt/java/openjdk; \
    cd /opt/java/openjdk; \
    tar -xf /tmp/openjdk.tar.gz --strip-components=1; \
    rm -rf /tmp/openjdk.tar.gz;

ENV JAVA_HOME=/opt/java/openjdk \
    PATH="/opt/java/openjdk/bin:$PATH"


# Bitbucket install
ENV RUN_USER            					daemon
ENV RUN_GROUP           					daemon

# https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+home+directory
ENV BITBUCKET_HOME          				/var/atlassian/application-data/bitbucket
ENV BITBUCKET_INSTALL_DIR   				/opt/atlassian/bitbucket

VOLUME ["${BITBUCKET_HOME}"]
WORKDIR $BITBUCKET_HOME

# Expose HTTP and SSH ports
EXPOSE 7990
EXPOSE 7999

# CMD ["/entrypoint.sh", "-fg"]
# ENTRYPOINT ["/tini", "--"]

RUN apt-get update \
	&& apt-get install -y --no-install-recommends fontconfig git perl procps \
	&& apt-get clean autoclean && apt-get autoremove -y && rm -rf /var/lib/apt/lists/*

ARG TINI_VERSION=v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

#  COPY entrypoint.sh             				/entrypoint.sh

ARG BITBUCKET_VERSION=6.3.0
ARG DOWNLOAD_URL=https://product-downloads.atlassian.com/software/stash/downloads/atlassian-bitbucket-${BITBUCKET_VERSION}.tar.gz

RUN mkdir -p                             	${BITBUCKET_INSTALL_DIR} \
    && curl -L --silent                  	${DOWNLOAD_URL} | tar -xz --strip-components=1 -C "${BITBUCKET_INSTALL_DIR}" \
    && chown -R ${RUN_USER}:${RUN_GROUP} 	${BITBUCKET_INSTALL_DIR}/ \
    && sed -i -e 's/^# umask/umask/' 		${BITBUCKET_INSTALL_DIR}/bin/_start-webapp.sh

CMD ["/opt/atlassian/bitbucket/bin/start-bitbucket.sh","run"] 