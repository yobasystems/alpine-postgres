FROM yobasystems/alpine:3.23.0-aarch64

ARG BUILD_DATE
ARG VCS_REF
ARG POSTGRES_VERSION=18
ARG POSTGRES_FULL_VERSION=18.1

LABEL maintainer="Dominic Taylor <dominic@yoba.systems>" \
    architecture="arm64v8/aarch64" \
    postgres-version="${POSTGRES_FULL_VERSION}" \
    alpine-version="3.23.0" \
    build="04-Dec-2025" \
    org.opencontainers.image.title="alpine-postgres" \
    org.opencontainers.image.description="Postgresql container image running on Alpine Linux" \
    org.opencontainers.image.authors="Dominic Taylor <dominic@yoba.systems>" \
    org.opencontainers.image.vendor="Yoba Systems" \
    org.opencontainers.image.version="${POSTGRES_FULL_VERSION}" \
    org.opencontainers.image.url="https://hub.docker.com/r/yobasystems/alpine-postgres/" \
    org.opencontainers.image.source="https://github.com/yobasystems/alpine-postgres" \
    org.opencontainers.image.base.name="docker.io/yobasystems/alpine:3.23.0" \
    org.opencontainers.image.revision=$VCS_REF \
    org.opencontainers.image.created=$BUILD_DATE

ENV LANG=en_GB.utf8
ENV PGDATA=/var/lib/postgresql/data

# postgresql-url_encode versions: PG16=alpine 3.20, PG17=alpine 3.22, PG18=alpine 3.23
ARG EXTENSIONS_REPO=https://dl-cdn.alpinelinux.org/alpine/v3.23/community
RUN apk update && \
    apk add su-exec postgresql${POSTGRES_VERSION} && \
    echo "@extensions ${EXTENSIONS_REPO}" >> /etc/apk/repositories && \
    apk add postgresql-url_encode@extensions postgresql-pgvector@extensions postgresql-hypopg@extensions postgresql-pg_cron@extensions && \
    mkdir /docker-entrypoint-initdb.d && \
    rm -rf /var/cache/apk/*

VOLUME /var/lib/postgresql/data

COPY files/docker-entrypoint.sh /

RUN chmod -R 755 /docker-entrypoint.sh && \
    mkdir -p /run/postgresql && \
    chown postgres: /run/postgresql

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
