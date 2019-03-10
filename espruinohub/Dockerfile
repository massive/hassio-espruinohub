# ARG BUILD_FROM=hassioaddons/base:2.3.2
# FROM ${BUILD_FROM}
FROM hassioaddons/base:2.3.2

ENV LANG C.UTF-8

USER root

ARG BUILD_ARCH

RUN \
    apk add --no-cache \
    nodejs=8.14.0-r0 \
    npm=8.14.0-r0 \
    git=2.18.1-r0 \
    python=2.7.15-r1 \
    build-base=0.5-r1 \
    bluez=5.49-r2 \
    linux-headers=4.4.6-r2 \
    eudev-dev=3.2.5-r2

RUN git clone https://github.com/espruino/EspruinoHub /var/espruinohub

WORKDIR /var/espruinohub

RUN npm install --unsafe-perm

COPY run.sh /var/espruinohub/run.sh
RUN chmod +x /var/espruinohub/run.sh

CMD /var/espruinohub/run.sh