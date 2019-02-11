FROM yobasystems/alpine:3.9.0-amd64
LABEL maintainer "Dominic Taylor <dominic@yobasystems.co.uk>" architecture="AMD64/x86_64"
LABEL postgres-version="11.1" alpine-version="3.9.0" date="11-Feb-2018"

ENV LANG en_GB.utf8
ENV PGDATA /var/lib/postgresql/data

RUN apk update && \
    apk add su-exec tzdata libpq postgresql-client postgresql postgresql-contrib && \
    mkdir /docker-entrypoint-initdb.d && \
    rm -rf /var/cache/apk/*


VOLUME /var/lib/postgresql/data

COPY files/docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
