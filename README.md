# Mantle

[![Travis](https://img.shields.io/travis/hivelocityinc/mantle.svg?style=flat-square)](https://travis-ci.org/hivelocityinc/mantle)
[![Docker Pulls](https://img.shields.io/docker/pulls/hivelocityinc/mantle.svg?maxAge=2592000?style=flat-square)](https://hub.docker.com/r/hivelocityinc/mantle/)

The Dockerfile for development environment with LEMP Stack.

## Requirements

- **Docker**
  - [For Mac](https://docs.docker.com/docker-for-mac/)
  - [For Windows](https://docs.docker.com/docker-for-windows/)

## Includes

It is based on Alpine Linux and includes middleware of the following:

- **Supervisor** : 3.2.0
- **Nginx** : 1.10
- **PHP** : 5.6
- **MySQL(MariaDB)** : 10.1
- **Memcached** : 1.4
- **Redis** : 3.2


## Basic Usage

```bash
$ docker pull hivelocityinc/mantle
$ docker run -d \
  --name mantle \
  -p 80:80 \
  -p 443:443 \
  -p 3306:3306 \
  -v $PWD/{your_app_dir}:/var/www/html/{app_name}
  hivelocityinc/mantle
```

## Configuration

You can change the config of middleware when you set environment value of the following:

| ENV Key | Default Value | Description |
|:---|:---|:---|
| **NGINX_WORKER_PROCESSES** | `1` | Ningx: worker processes |
| **NGINX_SERVER_NAME** | `localhost` | Ningx: server name |
| **NGINX_DOCUMENT_ROOT** | `/usr/share/nginx/html` | Nginx: document root path |
| **MYSQL_ROOT_PASSWORD** | `root` | MySQL: root user's password |
| **MYSQL_DATABASE** | `mantle` | MySQL: database name |
| **MYSQL_USER** | `mantle` | MySQL: database user |
| **MYSQL_PASSWORD** | `mantle` | MySQL: database password for $MYSQL_USER |
| **MEMCACHED_MEMUSAGE** | `64` | Memcached: memory usage size |
| **MEMCACHED_MAXCONN** | `1024`| Memcached: maximum number of concurrent connections |

### Import DB data
If you want to import databases data to container, to add `/initdb.d/schema` or `/initdb.d/sheeds` volume.

```bash
# Example
$ docker run -d \
  -v $PWD/{your_schema_dir}:/initdb.d/schema \
  -v $PWD/{your_seed_dir}:/initdb.d/sheeds \
  hivelocityinc/mantle
```

## Develop

Firstly, you have to install a gem package for Serverspec.

```bash
$ bundle install vendor/bundle
```

**Build image from Dockerfile**

```bash
$ sh ./script/docker.sh build

# OR
$ docker build -t hivelocityinc/mantle .
```

**Run container**

```bash
$ sh ./script/docker.sh run

# OR
$ docker run -d \
  --name mantle
  -p 80:80
  hivelocityinc/mantle
```

**Clean up to image and container**

```bash
$ sh ./script/docker.sh clean

# OR
$ docker kill mantle
$ docker rm mantle
$ docker rmi hivelocityinc/mantle
```

**Testing**

```bash
$ sh ./script/docker.sh test

# OR
$ bundle exec rake
```
