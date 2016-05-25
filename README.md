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

Run `docker-machine ls` to ensure you see the newley created `docker-vm`.



