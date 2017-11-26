# Postgres Docker image running on Alpine Linux

[![Docker Layers](https://img.shields.io/badge/docker%20layers-3-blue.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-postgres/) [![Docker Size](https://img.shields.io/badge/docker%20size-10%20MB-blue.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-postgres/) [![Docker Stars](https://img.shields.io/docker/stars/yobasystems/alpine-postgres.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-postgres/) [![Docker Pulls](https://img.shields.io/docker/pulls/yobasystems/alpine-postgres.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/yobasystems/alpine-postgres/)

[![Alpine Version](https://img.shields.io/badge/alpine%20version-v3.6.2-green.svg?maxAge=2592000?style=flat-square)](http://alpinelinux.org/) [![Postgres Version](https://img.shields.io/badge/Postgres%20version-v9.6.6-green.svg?maxAge=2592000?style=flat-square)](https://www.postgresql.org/)


This Docker image [(yobasystems/alpine-postgres)](https://hub.docker.com/r/yobasystems/alpine-postgres/) is based on the minimal [Alpine Linux](http://alpinelinux.org/) with [Postgres 9.6.6](https://www.postgresql.org/) object-relational database server.

##### Alpine Version 3.6.2 (Released Jun 17, 2017)
##### Postgres Version 9.6.6

----

## What is Alpine Linux?
Alpine Linux is a Linux distribution built around musl libc and BusyBox. The image is only 5 MB in size and has access to a package repository that is much more complete than other BusyBox based images. This makes Alpine Linux a great image base for utilities and even production applications. Read more about Alpine Linux here and you can see how their mantra fits in right at home with Docker images.

## What is Postgres?
PostgreSQL, often simply "Postgres", is an object-relational database management system (ORDBMS) with an emphasis on extensibility and standards-compliance. As a database server, its primary function is to store data, securely and supporting best practices, and retrieve it later, as requested by other software applications, be it those on the same computer or those running on another computer across a network (including the Internet). It can handle workloads ranging from small single-machine applications to large Internet-facing applications with many concurrent users. Recent versions also provide replication of the database itself for security and scalability.

## Features

* Minimal size only 10 MB and only 3 layers
* Memory usage is minimal on Alpine Linux.
* Postgresql Version 9.6.6
* Armv7 (armhf) version with ```:armhf``` tag

## Architectures

* ```:amd64```, ```:latest``` - 64 bit Intel/AMD (x86_64/amd64)
* ```:i386```, ```:x86``` - 32 bit Intel/AMD (x86/i686)
* ```:arm64v8```, ```:aarch64``` - 64 bit ARM (ARMv8/aarch64)
* ```:arm32v7```, ```:armhf``` - 32 bit ARM (ARMv7/armhf)

#### PLEASE CHECK TAGS BELOW FOR SUPPORTED ARCHITECTURES, THE ABOVE IS A LIST OF EXPLANATION

## Tags

* ```:latest```, ```:amd64``` latest branch based on amd64
* ```:master``` master branch usually inline with latest
* ```:v0.0.0``` version number related to docker version
* ```:armhf```, ```:arm32v7``` Armv7 based on latest tag but arm architecture

## Volume structure

* `/var/lib/postgresql/data`: Database files

## Environment Variables:

The PostgreSQL image uses several environment variables which are easy to miss. While none of the variables are required, setting a password as a minimum will ensure some degree of security when using the image.

### Main Postgres parameters:
* `POSTGRES_PASSWORD`: This environment variable is recommended for you to use the PostgreSQL image. This environment variable sets the superuser password for PostgreSQL. The default superuser is defined by the POSTGRES_USER environment variable. In the above example, it is being set to "RaNd0MpA55W0Rd".
* `POSTGRES_USER`: This optional environment variable is used in conjunction with POSTGRES_PASSWORD to set a user and its password. This variable will create the specified user with superuser power and a database with the same name. If it is not specified, then the default user of "postgres" will be used.
* `PGDATA`: This optional environment variable can be used to define another location - like a subdirectory - for the database files. The default is /var/lib/postgresql/data, but if the data volume you're using is a fs mountpoint (like with GCE persistent disks), Postgres initdb recommends a subdirectory (for example /var/lib/postgresql/data/pgdata ) be created to contain the data.
* `POSTGRES_DB`: This optional environment variable can be used to define a different name for the default database that is created when the image is first started. If it is not specified, then the value of POSTGRES_USER will be used.
* `POSTGRES_INITDB_ARGS`: This optional environment variable can be used to send arguments to postgres initdb. The value is a space separated string of arguments as postgres initdb would expect them. This is useful for adding functionality like data page checksums: -e POSTGRES_INITDB_ARGS="--data-checksums".

> https://www.postgresql.org/

## Creating an instance

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=RaNd0MpA55W0Rd -d yobasystems/alpine-postgres
```

It will create a new db called "postgres", with user "postgres" and set root password of "RaNd0MpA55W0Rd".

## Docker Compose example:

####(Please pass your own credentials, don't use these ones for production!!)

```yalm
mysql:
  image: yobasystems/alpine-postgres
  environment:
    POSTGRES_DB: salesdb
    POSTGRES_USER: johnsmith
    POSTGRES_PASSWORD=RaNd0MpA55W0Rd
  expose:
    - "5432"
  volumes:
    - /data/postgres/pgdata:/var/lib/postgresql/data
  restart: always
```

## Source Repository

* [Bitbucket - yobasystems/alpine-postgres](https://bitbucket.org/yobasystems/alpine-postgres/)

* [Github - yobasystems/alpine-postgres](https://github.com/yobasystems/alpine-postgres)

## Links

* [Yoba Systems](https://www.yobasystems.co.uk/)

* [Dockerhub - yobasystems](https://hub.docker.com/u/yobasystems/)

* [Quay.io - yobasystems](https://quay.io/organization/yobasystems)
