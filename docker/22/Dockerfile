FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:22-jdk-noble

LABEL       author="XJIuPa" maintainer="egg@xjiupa.com"
LABEL       org.opencontainers.image.source="https://github.com/gravit-core/gravit-eggs"

USER        root

RUN         apt update -y \
            && apt install -y \
                curl \
                lsof \
                ca-certificates \
                openssl \
                git \
                tar \
                sqlite3 \
                fontconfig \
                tzdata \
                iproute2 \
                libfreetype6 \
                tini \
                zip \
                unzip \
                osslsigncode \
                bash \
                unzip \
            && curl -sL https://sentry.io/get-cli/ | sh \
            && sentry-cli update

ENV         JMODS_DIR=/usr/share/openjfx/jmods
ENV         JMODS_URL=https://download2.gluonhq.com/openjfx/22/openjfx-22_linux-x64_bin-jmods.zip

RUN         ln -s /opt/java/openjdk-* /opt/java/openjdk

RUN         curl -L ${JMODS_URL} -o openjfx.zip \
            && unzip openjfx.zip && rm openjfx.zip \
            && mkdir -p ${JMODS_DIR} \
            && cp javafx-jmods-22/* /usr/share/openjfx/jmods

RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
