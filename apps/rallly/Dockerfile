FROM --platform=linux/amd64 public.ecr.aws/docker/library/node:18-alpine as builder

WORKDIR /tmp/rallly
#hadolint ignore=DL3018
RUN apk add --no-cache git \
    && git clone --depth 1 https://github.com/lukevella/rallly . \
    && cp sample.env .env \
    && cp prisma/schema.prisma . \
    && yarn --frozen-lockfile \
    && yarn build


FROM ghcr.io/ndmacioce/alpine:rolling@sha256:803cf73485c2fd673087854c051f07ff5a219f732780cbe98cfd497470524d3f
COPY --from=builder /tmp/rallly .
RUN apk add --no-cache yarn
USER kah
CMD sh -c "yarn start"
LABEL org.opencontainers.image.source="https://github.com/lukevella/rallly"
