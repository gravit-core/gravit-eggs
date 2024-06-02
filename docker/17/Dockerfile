FROM        --platform=$TARGETOS/$TARGETARCH ghcr.io/pelican-eggs/yolks:java_17

LABEL       author="XJIuPa" maintainer="egg@xjiupa.com"
LABEL       org.opencontainers.image.source="https://github.com/gravit-core/gravit-eggs"

RUN         apt-get update -y \
			&& apt-get install -y curl lsof ca-certificates openssl osslsigncode git tar bash sqlite3 fontconfig tzdata iproute2 libfreetype6 \
            && curl -sL https://sentry.io/get-cli/ | sh \
            && sentry-cli update

ENV         JMODS_DIR=/usr/share/openjfx/jmods
ENV         JMODS_URL=https://download2.gluonhq.com/openjfx/17.0.11/openjfx-17.0.11_linux-x64_bin-jmods.zip

RUN         curl -L ${JMODS_URL} -o openjfx.zip \
            && unzip openjfx.zip && rm openjfx.zip \
            && mkdir -p ${JMODS_DIR} \
            && cp javafx-jmods-17.0.2/* /usr/share/openjfx/jmods

RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
