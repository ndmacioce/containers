FROM ghcr.io/ndmacioce/alpine:rolling@sha256:b16ce8185c1c93d7563842e60c2d189f3d0ff9d4b9fab83d1104c93d49ee30e5

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
