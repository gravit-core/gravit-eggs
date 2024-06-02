FROM        --platform=$TARGETOS/$TARGETARCH ghcr.io/pelican-eggs/yolks:java_21

LABEL       author="XJIuPa" maintainer="egg@xjiupa.com"
LABEL       org.opencontainers.image.source="https://github.com/gravit-core/gravit-eggs"

USER        root

RUN         apt-get update -y \
			&& apt-get install -y curl lsof ca-certificates openssl osslsigncode git tar bash sqlite3 fontconfig tzdata iproute2 libfreetype6 \
            && curl -sL https://sentry.io/get-cli/ | sh \
            && sentry-cli update

ENV         JMODS_DIR=/usr/share/openjfx/jmods
ENV         JMODS_URL=https://download2.gluonhq.com/openjfx/21.0.3/openjfx-21.0.3_linux-x64_bin-jmods.zip

RUN         curl -L ${JMODS_URL} -o openjfx.zip \
            && unzip openjfx.zip && rm openjfx.zip \
            && mkdir -p ${JMODS_DIR} \
            && cp javafx-jmods-21.0.3/* /usr/share/openjfx/jmods

USER        container
RUN         useradd -m -d /home/container -s /bin/bash container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
