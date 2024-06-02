FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:21-jdk-jammy

LABEL       author="XJIuPa" maintainer="egg@xjiupa.com"
LABEL       org.opencontainers.image.source="https://github.com/gravit-core/gravit-eggs"

RUN         apt-get update -y \
			&& apt-get install -y curl lsof ca-certificates openssl osslsigncode git tar bash sqlite3 fontconfig tzdata iproute2 libfreetype6 \
            && curl -sL https://sentry.io/get-cli/ | sh \
            && sentry-cli update

RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
