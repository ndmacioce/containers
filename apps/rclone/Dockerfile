FROM ghcr.io/ndmacioce/alpine:rolling@sha256:b16ce8185c1c93d7563842e60c2d189f3d0ff9d4b9fab83d1104c93d49ee30e5

ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG VERSION
ARG CHANNEL

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

#hadolint ignore=DL3018
RUN apk add --no-cache ca-certificates pigz rclone~"${VERSION}" tar zstd
#hadolint ignore=DL3059
RUN chown -R root:root /usr/bin/rclone \
    && chmod -R 755 /usr/bin/rclone \
    && ln -s /usr/bin/rclone /app/rclone \
    && rm -rf /tmp/*

CMD ["/app/rclone"]

LABEL org.opencontainers.image.source="https://github.com/rclone/rclone"
