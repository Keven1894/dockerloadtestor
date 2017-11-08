# Locusts Docker Image

The locusts docker image is designed for easily composing multi-container 
[locust.io](http://http://locust.io/) 
load testing swarms using Python 3.6. The locusts image functions can function
as either a master or worker depending on whether or not the `--master-host` 
flag is specified in a container's run execution call.

The original docker image is available in 
[Docker Hub](https://hub.docker.com/r/swernst/locusts/). You can pull the 
image with the command:

```bash
$ docker pull swernst/locusts:latest
```

This code was modified by Boyuan (Keven) Guan to test Docker Compose with 
work load test. The image is available at:

```bash
$ docker pull keven1894/loadtestor:latest
```

## Prepare Environment
You need to check if both [Docker](https://docs.docker.com/engine/installation/linux/ubuntu/) and [Docker Compose](https://docs.docker.com/compose/install/) are installed on your ubuntu box.

## Quick Start 
To test in your cluster is very simple, just clone the repository

```bash
$ git clone https://github.com/Keven1894/dockerloadtestor
```

Then move to the project folder:

```bash
$ cd dockerloadtestor
```

And start the docker-compose service by calling:

```bash
$ sudo docker-compose up
```

Once all the master and worder are loaded, you can go to http://0.0.0.0:8089 to test your cluster.

## Master & Workers

The optional `--master-host` argument is used to specify that the container 
should be a worker and communicate with the master with the specified host.
For example:

```bash
$ docker run -it --rm \
    -v ./scripts:/scripts \
    keven1894/loadtestor \
    --master-host=127.0.0.1
```

would specify a worker container where the master resides at the local
`127.0.0.1` host location.

## Script Volume

A locusts container requires that a volume be mounted to the container's 
`/scripts` directory. It expects to find the *locustfile.py* to run in that 
directory.

## Docker Compose

The multi-container environment is easily specified using docker compose. You 
can see an example in this repository of how that would look:
[docker-compose.yml](docker-compose.yml)
