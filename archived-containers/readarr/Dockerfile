FROM ghcr.io/ndmacioce/alpine:rolling@sha256:35a33771345f0437f5a78ed8bd870302b46cef8fb6cfb97a78406ff3f96e7e7b

ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG VERSION
ARG CHANNEL

ENV \
    READARR__INSTANCE_NAME="Readarr" \
    READARR__BRANCH="${CHANNEL}" \
    READARR__PORT="8787" \
    READARR__ANALYTICS_ENABLED="False"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

#hadolint ignore=DL3018
RUN apk add --no-cache ca-certificates icu-libs libintl sqlite-libs xmlstarlet
#hadolint ignore=DL3059
RUN \
    case "${TARGETPLATFORM}" in \
        'linux/amd64') export ARCH='x64' ;; \
        'linux/arm64') export ARCH='arm64' ;; \
    esac \
    && \
    curl -fsSL "https://readarr.servarr.com/v1/update/${READARR__BRANCH}/updatefile?version=${VERSION}&os=linuxmusl&runtime=netcore&arch=${ARCH}" \
        | tar xzf - -C /app --strip-components=1 \
    && \
    rm -rf \
        /app/Readarr.Update \
    && \
    printf "UpdateMethod=docker\nBranch=%s\nPackageVersion=%s\nPackageAuthor=[Team k8s-at-home](https://github.com/k8s-at-home)" "${READARR__BRANCH}" "${VERSION}" > /app/package_info \
    && chown -R root:root /app \
    && chmod -R 755 /app \
    && rm -rf /tmp/*

USER kah

COPY ./apps/readarr/config.xml.tmpl /app/config.xml.tmpl
COPY ./apps/readarr/entrypoint.sh /entrypoint.sh
CMD ["/entrypoint.sh"]

LABEL org.opencontainers.image.source="https://github.com/Readarr/Readarr"
