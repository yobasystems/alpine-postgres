# Postgres container image running on Alpine Linux

[![Docker Automated build](https://img.shields.io/docker/automated/yobasystems/alpine-postgres.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-postgres/)
[![Docker Pulls](https://img.shields.io/docker/pulls/yobasystems/alpine-postgres.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-postgres/)
[![Docker Stars](https://img.shields.io/docker/stars/yobasystems/alpine-postgres.svg?style=for-the-badge&logo=docker)](https://hub.docker.com/r/yobasystems/alpine-postgres/)

[![Alpine Version](https://img.shields.io/badge/Alpine%20version-v3.19.0-green.svg?style=for-the-badge&logo=alpine-linux)](https://alpinelinux.org/)
[![Postgres Version](https://img.shields.io/badge/Postgres%20version-v15.5-green.svg?style=for-the-badge&logo=postgres)](https://www.postgresql.org/)


This container image [(yobasystems/alpine-postgres)](https://hub.docker.com/r/yobasystems/alpine-postgres/) is based on the minimal [Alpine Linux](http://alpinelinux.org/) with [Postgres 15.5](https://www.postgresql.org/) object-relational database server.

### Alpine Version 3.19.0 (Released 2023-12-07)
##### Postgres Version 15.5

----

## Table of Contents

- [What is Alpine Linux?](#what-is-alpine-linux)
- [Features](#features)
- [Architectures](#architectures)
- [Tags](#tags)
- [Layers & Sizes](#layers--sizes)
- [How to use this image](#how-to-use-this-image)
- [Image contents & Vulnerability analysis](#image-contents--vulnerability-analysis)
- [Source Repositories](#source-repositories)
- [Container Registries](#container-registries)
- [Links](#links)
- [Donation](#donation)


## 🏔️ What is Alpine Linux?
Alpine Linux is a Linux distribution built around musl libc and BusyBox. The image is only 5 MB in size and has access to a package repository that is much more complete than other BusyBox based images. This makes Alpine Linux a great image base for utilities and even production applications. Read more about Alpine Linux here and you can see how their mantra fits in right at home with Docker images.

## What is Postgres?
PostgreSQL, often simply "Postgres", is an object-relational database management system (ORDBMS) with an emphasis on extensibility and standards-compliance. As a database server, its primary function is to store data, securely and supporting best practices, and retrieve it later, as requested by other software applications, be it those on the same computer or those running on another computer across a network (including the Internet). It can handle workloads ranging from small single-machine applications to large Internet-facing applications with many concurrent users. Recent versions also provide replication of the database itself for security and scalability.

## ✨ Features

* Minimal size only, minimal layers
* Memory usage is minimal on a simple install.

## 🏗️ Architectures

* ```:amd64```, ```:x86_64``` - 64 bit Intel/AMD (x86_64/amd64)
* ```:arm64v8```, ```:aarch64``` - 64 bit ARM (ARMv8/aarch64)
* ```:arm32v7```, ```:armhf``` - 32 bit ARM (ARMv7/armhf)

#### 📝 PLEASE CHECK TAGS BELOW FOR SUPPORTED ARCHITECTURES, THE ABOVE IS A LIST OF EXPLANATION

## 🏷️ Tags

* ```:latest``` latest branch based (Automatic Architecture Selection)
* ```:master``` master branch usually inline with latest
* ```:amd64```, ```:x86_64```  amd64 based on latest tag but amd64 architecture
* ```:aarch64```, ```:arm64v8``` Armv8 based on latest tag but arm64 architecture
* ```:armhf```, ```:arm32v7``` Armv7 based on latest tag but arm32 architecture

## 📏 Layers & Sizes

![Version](https://img.shields.io/badge/version-amd64-blue.svg?style=for-the-badge)
![MicroBadger Layers (tag)](https://img.shields.io/docker/layers/yobasystems/alpine-postgres/amd64.svg?style=for-the-badge)
![MicroBadger Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-postgres/amd64.svg?style=for-the-badge)

![Version](https://img.shields.io/badge/version-aarch64-blue.svg?style=for-the-badge)
![MicroBadger Layers (tag)](https://img.shields.io/docker/layers/yobasystems/alpine-postgres/aarch64.svg?style=for-the-badge)
![MicroBadger Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-postgres/aarch64.svg?style=for-the-badge)

![Version](https://img.shields.io/badge/version-armhf-blue.svg?style=for-the-badge)
![MicroBadger Layers (tag)](https://img.shields.io/docker/layers/yobasystems/alpine-postgres/armhf.svg?style=for-the-badge)
![MicroBadger Size (tag)](https://img.shields.io/docker/image-size/yobasystems/alpine-postgres/armhf.svg?style=for-the-badge)

## Volume structure

* `/var/lib/postgresql/data`: Database files

## 🚀 How to use this image
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
  image: yobasystems/alpine-postgres:15.5
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

## 🔍 Image contents & Vulnerability analysis

| PACKAGE NAME          | PACKAGE VERSION | VULNERABILITIES |
|-----------------------|-----------------|-----------------|


## 📚 Source Repositories

* [Github - yobasystems/alpine-postgres](https://github.com/yobasystems/alpine-postgres)

* [Gitlab - yobasystems/alpine-postgres](https://gitlab.com/yobasystems/alpine-postgres)

* [Bitbucket - yobasystems/alpine-postgres](https://bitbucket.org/yobasystems/alpine-postgres/)


## 🐳 Container Registries

* [Dockerhub - yobasystems/alpine-postgres](https://hub.docker.com/r/yobasystems/alpine-postgres/)

* [Quay.io - yobasystems/alpine-postgres](https://quay.io/repository/yobasystems/alpine-postgres)


## 🔗 Links

* [Yoba Systems](https://www.yobasystems.co.uk/)

* [Github - Yoba Systems](https://github.com/yobasystems/)

* [Dockerhub - Yoba Systems](https://hub.docker.com/u/yobasystems/)

* [Quay.io - Yoba Systems](https://quay.io/organization/yobasystems)

* [Maintainer - Dominic Taylor](https://github.com/dominictayloruk)

## 💰 Donation

[![BMAC](https://img.shields.io/badge/BUY%20ME%20A%20COFFEE-£5-blue.svg?style=for-the-badge&logo=buy-me-a-coffee)](https://www.buymeacoffee.com/dominictayloruk?new=1)

[![BITCOIN](https://img.shields.io/badge/BTC-bc1q7hy8qmyvq7rw6slrna7yffcdnj9rcg4e9xjecc-blue.svg?style=for-the-badge&logo=bitcoin)](bitcoin:bc1q7hy8qmyvq7rw6slrna7yffcdnj9rcg4e9xjecc)

[![ETHEREUM](https://img.shields.io/badge/ETH-0xb6bE2e4da3d86b50Bdae1F9B6960c23dd87C532C-blue.svg?style=for-the-badge&logo=ethereum)](ethereum:0xb6bE2e4da3d86b50Bdae1F9B6960c23dd87C532C)
