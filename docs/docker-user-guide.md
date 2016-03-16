# Docker Multiple Container User Guide

### Introduction

This document covers briefly how to run the multiple containers version of
Islandora.

If you wish to run the single container version please follow the guide provided
[here](../images/all-in-one).

Also checkout our [Development Guide](docker-development.md) if you plan on
doing some development work.

### Vagrant

Vagrant is a tool for building complete development environments, that run on
either Virtualbox or in a cloud service like Digital Ocean or AWS. It also
allows you to manage your environments with ```vagrant``` commands.

We provide an a Vagrant file in this repositories top level directory. It will
bring up a Ubuntu based image, install Docker and Docker-Compose on the machine,
as well as pull down all the required images to get started.

It's useful for those:

1. Who are not using [Docker Toolbox](/install-guide.md#docker-toolbox), and
prefer to keep Vagrant as the only dependency.

2. For those who wish not to use the Virtual Machine bundled with Docker Toolbox
(boot2docker), and prefer to use the same host OS they will use in production.

3. For those who want to utilize other Vagrant features like
   [Vagrant Share](https://www.vagrantup.com/docs/share/).

**N.B.** You can still use Docker Machine with the provided Vagrant setup.
  Read the next section for more information.

**N.B.** If you do not install Docker Machine and install Docker Compose locally you
  will have to ssh into the server to interact with Docker.

### Docker Machine

[Docker Machine][docker-machine] is a tool that lets you install Docker on
virtual hosts, servers and linux machines. It also allows you to manage the
hosts with ```docker-machine``` commands.

#### Docker Toolbox

If you installed the [Docker Toolbox](/install-quide.md#docker-machine) you'll
already have this setup. 

You can either use launcher bundled with Docker Toolbox to set up your shell ENV
such that you can use the ```docker``` command. Or you can add the following to
your shell start-up scripts, so it's always available.

```bash
eval $(docker-machine env default);
```

Once you've done that you can use Docker and Docker Compose on your local
machine without ssh to any server anywhere.

**N.B.** You'll have to open Kitematic to start the Virtual Machine the first
  time.

#### Vagrant

If you wish to use Docker Machine with our provided Vagrant install your in luck
as it is setup automatically when you run ```vagrant up```, that is assuming you
have [Docker Machine installed](/install-guide.md#docker-machine).

You will still have to configure your Docker Machine install to point to your
vagrant instance by adding.

```bash
val $(docker-machine env islandora-claw-docker);
```

**N.B.** The Docker machine environment can be set to point to only a single
  machine at a time. 

#### Cloud / Server

This is out of the scope of this document but is covered at length by the
[Docker Machine Documentation](https://docs.docker.com/machine/get-started-cloud/).

### Docker Compose

[Docker Compose] is a tool for defining and running multi-container Docker
applications (though it can be used for single container applications as well).

We use it for both our single and multi-container versions of Islandora, though
it's not required for the single container version.

We provide a ```docker-compose.yml``` file at the top level, can be used to pull
down all the required images to run Islandora as well as to start, stop, restart
and scale individual containers.

Some quick basics (run from the top level directory of this repository):

**Pull down latest images:**
```bash
docker-compose pull
```

**Start application in foreground:** 
```bash
docker-compose up
```

**Start application in background:** 
```bash
docker-compose up -d
```

**Stop application (containers still exist but are stopped):** 
```bash
docker-compose stop
```

**Remove stopped containers):** 
```bash
docker-compose rm
```

Checkout the [Docker Compose documentation][docker-compose-docs] for more info.

### Reference Material

* [Docker Documentation][docker-docs]
* [Docker Compose Documentation][docker-compose-docs]
* [Docker Machine Documentation][docker-machine-docs]
* [Vagrant Documentation][vagrant-docs]
