ARG BUILD_FROM=ghcr.io/hassio-addons/base:12.2.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

WORKDIR /app

RUN \
    apk add --no-cache \
        nodejs=16.16.0-r0 \
        npm=8.10.0-r0 \
    \
    && E2M="1.3.0"\
    && curl -L -o /tmp/e2m.tar.gz https://github.com/thevoltagesource/eagle-mqtt-bridge/archive/refs/tags/v${E2M}.tar.gz \
    && tar -xvzf /tmp/e2m.tar.gz -C /tmp \
    && cp /tmp/eagle-mqtt-bridge-${E2M}/*.js* . \
    && npm ci \
    \
    && rm -rf /tmp/*

COPY rootfs /