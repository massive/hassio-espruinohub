ARG BUILD_FROM=hassioaddons/base:5.0.1
FROM ${BUILD_FROM}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV LANG C.UTF-8

USER root

ARG BUILD_ARCH

RUN \
    apk add --no-cache \
        nodejs=10.16.3-r0 \
        npm=10.16.3-r0 \
        python=2.7.16-r1 \
        build-base=0.5-r1 \
        bluez=5.50-r3 \
        linux-headers=4.19.36-r0 \
        eudev-dev=3.2.8-r0 \
    && apk add --no-cache --virtual .build-dependencies \
        git=2.22.0-r0 \
    \
    && npm set unsafe-perm true \
    && VERSION="76753003df534b32d2e9dad9fa74aeb0e93876a1" \
    && NODE_PATH="/usr/lib/node_modules" \
    && npm -g i \
        "git+https://github.com/espruino/EspruinoHub.git#${VERSION}" \
    \
    && apk del --no-cache --purge .build-dependencies

# Copy root file system
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

WORKDIR /var/espruinohub

COPY run.sh /var/espruinohub/run.sh
RUN chmod +x /var/espruinohub/run.sh

CMD /var/espruinohub/run.sh

# Labels
LABEL \
    io.hass.name="EspruinoHub" \
    io.hass.description="BLE MQTT bridge" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Matias Käkelä" \
    org.label-schema.description="BLE MQTT bridge" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="EspruinoHub" \
    org.label-schema.schema-version="0.4.0" \
    org.label-schema.usage="https://github.com/massive/hassio-espruinohub/blob/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/massive/hassio-espruinohub.git" \
    org.label-schema.vendor="Community Hass.io Addons"