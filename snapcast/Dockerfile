##ARG BUILD_FROM
#FROM $BUILD_FROM
FROM ghcr.io/home-assistant/i386-base-python:3.12-alpine3.20
#FROM evthefuture/hassio-addon-snapcast-i386
ENV LANG C.UTF-8

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy data for add-on
COPY rootfs /

RUN apk update
RUN apk add --no-cache openrc
RUN apk add --no-cache snapcast snapcast-server snapcast-client
#RUN apk add --no-cache librespot
RUN apk add --no-cache alsa-plugins-pulse flac  libflac openrc avahi-libs
#RUN apk add --no-cache neovim screen
