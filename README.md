# WIP: Mantle

[![Travis](https://img.shields.io/travis/hivelocityinc/mantle.svg?style=flat-square)](https://travis-ci.org/hivelocityinc/mantle)

The Dockerfile for development environment with LEMP Stack.


## Includes

It is based on Alpine Linux and includes middleware of the following:

- **Supervisor** : 3.2.0
- **Nginx** : 1.10.1
- PHP 5.6
- MySQL(MariaDB)


## Usage

```bash
$ docker run -d \
  --name mantle
  -p 80:80
  hivelocityinc/mantle
```

## Configuration

| ENV | default | Description |
|:---|:---|
| WORKER_PROCESSES | `1` | nginx werker_processes |
| SERVER_NAME | `localhost` | your site's hostname |

## Develop

Firstly, you have to install a gem package for Serverspec.

```bash
$ bundle install vendor/bundle
```

### Build image from Dockerfile

```bash
$ sh ./script/docker.sh build

# OR
$ docker build -t hivelocityinc/mantle .
```

### Run container

```bash
$ sh ./script/docker.sh run

# OR
$ docker run -d \
  --name mantle
  -p 80:80
  hivelocityinc/mantle
```

### Clean up to image and container

```bash
$ sh ./script/docker.sh clean

# OR
$ docker kill mantle
$ docker rm mantle
$ docker rmi hivelocityinc/mantle
```

### Testing

```bash
$ sh ./script/docker.sh test

# OR
$ bundle exec rake
```
