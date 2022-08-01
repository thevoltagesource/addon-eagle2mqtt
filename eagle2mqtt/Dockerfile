ARG BUILD_FROM=ghcr.io/hassio-addons/base:12.2.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]


RUN \
	E2M = "1.3.0"\
	\
    apk add --no-cache \
        nodejs=16.16.0-r0 \
        npm=8.10.0-r0 \
    \
    && curl -L -o /tmp/e2m.tar.gz https://github.com/thevoltagesource/eagle-mqtt-bridge/archive/refs/tags/v${E2M}.tar.gz \
    \
    && tar -xvz /tmp/e2m.tar.gz -C /tmp \
    \
    && cp /tmp/eagle-mqtt-bridge-${E2M}/*.js* . \
    \
    && npm ci \
    \
    rm -rf /tmp/*

# Copy root filesystem
COPY rootfs /

# Health check
HEALTHCHECK CMD curl --fail http://127.0.0.1:3000 || exit 1

