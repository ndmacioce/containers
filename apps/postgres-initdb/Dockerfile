FROM ghcr.io/ndmacioce/alpine:rolling@sha256:3698207b9d8bbab74d9f57042164f6adefef3141532a6c3d52f967b73678a1ad

ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG VERSION
ARG CHANNEL

ENV POSTGRES_SUPER_USER="postgres" \
    POSTGRES_RESET="false" \
    POSTGRES_USER_RESET="false" \
    POSTGRES_RESET_CONFIRM="NO"

#hadolint ignore=DL3018
RUN apk add --no-cache ca-certificates postgresql14-client~"${VERSION}"

USER kah

COPY ./apps/postgres-initdb/entrypoint.sh /entrypoint.sh

CMD ["/entrypoint.sh"]

LABEL org.opencontainers.image.source="https://github.com/postgres/postgres"
