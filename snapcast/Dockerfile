ARG BUILD_FROM
FROM $BUILD_FROM
#FROM ghcr.io/home-assistant/i386-base-python:3.12-alpine3.20
ENV LANG C.UTF-8

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy data for add-on
#COPY rootfs /

RUN printf "@edge http://dl-cdn.alpinelinux.org/alpine/edge/testing\n@edgeC http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories  

RUN apk update
RUN apk add --no-cache openrc
RUN apk add --no-cache alsa-plugins-pulse flac  libflac openrc avahi-libs
RUN apk add --no-cache snapcast-client@edgeC snapcast-server@edgeC
RUN apk add --no-cache librespot@edge
#RUN apk add --no-cache shairport-sync@edgeC

RUN mkdir /etc/services.d/snapclient
COPY snapclient-run /etc/services.d/snapclient/run
RUN chmod +x /etc/services.d/snapclient/run

RUN mkdir /etc/services.d/snapserver
COPY snapserver-run /etc/services.d/snapserver/run
RUN chmod +x /etc/services.d/snapserver/run

#ADD MPD and configure the input via pipe
RUN apk add --no-cache mpd
RUN printf "audio_output {\n    type            \"fifo\"\n    name            \"my pipe\"\n    path            \"/tmp/snapfifo\"\n    format          \"48000:16:2\"\n    mixer_type      \"software\"\n}"  >> /etc/mpd.conf

#Install Snapweb
RUN  cd /usr/share/snapserver/snapweb/ && wget https://github.com/badaix/snapweb/releases/download/v0.8.0/snapweb.zip && unzip -o snapweb.zip && rm snapweb.zip
