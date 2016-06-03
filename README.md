# docker

These are the instructions for setting up [Drupal Docker](https://hub.docker.com/_/drupal/).

## Requirements

- Install [Docker Toolbox](https://www.docker.com/products/docker-toolbox)

## Setup Docker Machine in Virtual Box

`$ docker-machine create --driver virtualbox docker-vm`

Add the output of that command to your `.bashrc` file.  Should look something like this:

```
  # Docker
  export DOCKER_TLS_VERIFY="1"
  export DOCKER_HOST="tcp://192.168.99.100:2376"
  export DOCKER_CERT_PATH="/Users/yourusername/.docker/machine/machines/docker-vm"
  export DOCKER_MACHINE_NAME="docker-vm"
```

### Verify install

Run `$ docker-machine ls` to ensure you see the newley created `docker-vm`.

## Setup Drupal process

`$ docker run --name some-drupal -p 8080:80 -d drupal`

## Setup Mysql

`$ docker run --name some-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=drupal8 -d mysql`

## Access Site

Check and see what the IP address is for your server

`$ docker-machine ls`

Visit the site in your browser http://yourIP:8080


## Create Docker Compose file

This will look at your active processes and create a config file.

`$ docker-compose config`

Expected output:

```
networks: {}
services:
  drupal:
    image: drupal
    network_mode: bridge
    ports:
    - 8080:80
  drupaldb:
    environment:
      MYSQL_DATABASE: druapl8
      MYSQL_ROOT_PASSWORD: root
    image: mysql
    network_mode: bridge
version: '2.0'
volumes: {}
```
 
Save the output to a file called `docker-compose.yml`

## Kitematic

### Failed install

If the machine refuses to start, it might mean that the certs are bad. Example of a bad cert:

```
default     *        virtualbox   Running   tcp://192.168.99.100:2376           Unknown   Unable to query docker version: Get https://192.168.99.100:2376/v1.15/version: x509: certificate is valid for 192.168.99.101, not 192.168.99.10
```

To regenerate cert:

```
docker-machine regenerate-certs default
```

Restart Kitematic

## Normal Development Setup

Create Container

docker run -dP -e TERM --name <container-name> -v <file-location> <image-name>

Create bash or Zsh container for editing files

docker run -it --rm -e TERM --volumes-from <container-name> <image-name> zsh
