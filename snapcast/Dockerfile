#ARG BUILD_FROM
#FROM $BUILD_FROM
FROM ghcr.io/home-assistant/i386-base-python:3.12-alpine3.20
ENV LANG C.UTF-8

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy data for add-on
#COPY rootfs /

RUN apk update
RUN apk add --no-cache openrc
RUN apk add --no-cache snapcast snapcast-server snapcast-client
#RUN apk add --no-cache librespot
RUN apk add --no-cache alsa-plugins-pulse flac  libflac openrc avahi-libs

RUN mkdir /etc/services.d/snapclient
COPY snapclient-run /etc/services.d/snapclient/run
RUN chmod +x /etc/services.d/snapclient/run

RUN mkdir /etc/services.d/snapserver
COPY snapserver-run /etc/services.d/snapserver/run
RUN chmod +x /etc/services.d/snapserver/run
