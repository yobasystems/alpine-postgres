FROM yobasystems/alpine:3.18.4-amd64

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Dominic Taylor <dominic@yoba.systems>" \
    architecture="amd64/x86_64" \
    postgres-version="15.4" \
    alpine-version="3.18.4" \
    build="04-Oct-2023" \
    org.opencontainers.image.title="alpine-postgres" \
    org.opencontainers.image.description="Postgresql container image running on Alpine Linux" \
    org.opencontainers.image.authors="Dominic Taylor <dominic@yoba.systems>" \
    org.opencontainers.image.vendor="Yoba Systems" \
    org.opencontainers.image.version="v15.4" \
    org.opencontainers.image.url="https://hub.docker.com/r/yobasystems/alpine-postgres/" \
    org.opencontainers.image.source="https://github.com/yobasystems/alpine-postgres" \
    org.opencontainers.image.revision=$VCS_REF \
    org.opencontainers.image.created=$BUILD_DATE

ENV LANG en_GB.utf8
ENV PGDATA /var/lib/postgresql/data

RUN apk update && \
    apk add su-exec tzdata libpq postgresql15 postgresql-url_encode && \
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
