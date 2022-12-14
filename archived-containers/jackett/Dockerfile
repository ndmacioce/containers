FROM ghcr.io/onedr0p/ubuntu:rolling@sha256:f9cf9b85251fded70455eed9aa09e91fa7e73890f7c59abcc889256e51531ce1

ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG VERSION
ARG CHANNEL

ENV XDG_CONFIG_HOME=/config

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# hadolint ignore=DL3008,DL3015,SC2039,SC2086
RUN \
    apt-get -qq update \
    && \
    apt-get -qq install -y \
        libicu66 \
        libssl1.1 \
    && \
    case "${TARGETPLATFORM}" in \
        'linux/amd64') export ARCH='AMDx64' ;; \
        'linux/arm64') export ARCH='ARM64' ;; \
    esac \
    && \
    curl -fsSL "https://github.com/Jackett/Jackett/releases/download/v${VERSION}/Jackett.Binaries.Linux${ARCH}.tar.gz" \
        | tar ixzf - -C /app --strip-components 1 \
    && \
    rm -rf \
        /app/JackettUpdater* \
    && \
    apt-get autoremove -y \
    && apt-get clean \
    && \
    rm -rf \
        /tmp/* \
        /var/lib/apt/lists/* \
        /var/tmp/ \
    && chown -R root:root /app \
    && chmod -R 755 /app \
    && printf "umask %d" "${UMASK}" >> /etc/bash.bashrc

USER kah
COPY ./apps/jackett/entrypoint.sh /entrypoint.sh
CMD ["/entrypoint.sh"]

LABEL org.opencontainers.image.source="https://github.com/Jackett/Jackett"
