FROM ghcr.io/ndmacioce/alpine:rolling@sha256:f85970c91d02c4e0beb6a252b880abf9ae48d91b929f7052206bd34e15544faa

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
