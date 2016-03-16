# Docker Overview

### Introduction

This is a light guide to Docker and the tools and terms used by Docker, it's
meant as a very brief overview, and as a guideline before digging into the
[Official Docker Documentation](docker-docs).

Please refer to our [Install Guide](/install-guide.md) to setup Docker on your
system.

### What is Docker Container

In simplistic terms a Docker container is a method by which we can package a
application and it's entire operating environment into a single bundle, which
can be run on any OS environment that supports Docker.

It's a virtualization technology, much like virtual machines, except it operates
a higher level. It doesn't virtualize hardware, it virtualizes a process. 

It runs on the same Linux kernel as the host operating system. Even though they
container runs on the same same Linux kernel as the OS, it's isolated from the
host, and the host is isolated from the container.

### What is an Docker Image

A Docker image can be thought of a snapshot of a file-system, Docker containers
are created from layers of Docker images. 

Docker images only allow for single parent hierarchical inheritance. So you
can't merge two Docker different Docker Images into a new one, they must be
stacked one on-top of the other.

Docker Images are read-only, so when you start a Docker container, changes to
the file system are not persisted to the image. If you want to save your changes
you must commit them to a new Docker image.

### What is Docker

Docker is at it's core two tools.

1. Docker Engine
2. Docker Client

#### Docker Engine

The Docker Engine is at the core off all the Docker tools. It's responsible for
creating Docker Images, and for executing and Managing Docker containers.

[Docker Engine Documentation](https://docs.docker.com/engine).

#### Docker Client

The client is command line tool and API that allows us to interact with the
Docker Engine.

[Docker CLI Documentation](https://docs.docker.com/engine/reference/commandline/cli).

### Why Docker? 

While it may seem on the face Docker is just a lighter version of a Virtual
Machine, but it is so much more. Let's focus on the benefits of adopting Docker for
users of Islandora specifically.

#### Sharing

The burden of configuring and maintaining the environment can be shared by the
entire community. Now we not only share the Islandora code but also the means to
easily deploy production quality systems.

#### Identical Environments

If everyone in our community is building on-top of the same Docker Images we
provide it can eliminate entire classes of problems people have had in the past
in running Islandora.

#### Testing & Development Time

We will have a test environment automatically generated and tied to every commit
made to the core project so for each pull request we can test against
100% the exact same environment.

If a new feature requires new dependencies to be installed, testers no longer
need to manually install the requirements to test.

Since it's so fast to deploy another environment you need not modify your own to
test another branch, simply spin up the other environment, and run both
simultaneously to test.

#### Fast Provisioning

Docker images are layered and cached so when building on top of existing images
is blindingly fast.

If an Institution's site is only comprised of only additional Drupal modules and
themes which is typically the case, their environment can be generated in less
than 5 minutes.

#### Fast Deployment

We've put a lot of effort into building small images, such that you can download
the entire application in approximately 700 MB.

If you have a 8 Mbps internet connection you should be able to download the
entire application, and start it in approximately 15 minutes. If you have an 50
Mbps internet connection it could be as little as 5 minutes.

Once it's download you can start and stop new environments is mere minutes, using
the downloaded and cached images.

#### Windows Support

This isn't such a big deal as we've always been able to run Islandora via a
Virtual Machine on these systems, and this is still the case now. That being
said the Virtual Machine required to run Docker (boot2docker) is very small and
consumes little to no extra resources.

#### Scale

Last but not least the true reason everyone want's Docker is the ability to
scale applications. 

Docker will make it trivial:

1. to run an Islandora stack across several servers.
2. to replicate services and balance load/work across them.
3. scale existing services up & down as needed.

If you have access to the computer power you can dramatically decrease the time
large migrations and batch ingestion will take.

For example a University could store their repository on campus, but when doing
a large scale ingestion (say 10's of TB of data) they could run the derivative
generation services in the cloud scaling out to hundreds of machines. Once the
ingestion was done they could scale back down to just their campus computing
environment, saving months and potentially years of time during the migration.
Not to mention potentially saving tens of thousands of Dollars in executing the
migration.

### Reference Material

* [Docker Documentation][docker-docs]
* [Docker Install Guide][docker-install]

[docker]: https://docker.com
[docker-docs]: https://docs.docker.com 
[docker-compose]: https://www.docker.com/products/docker-compose
[docker-compose-docs]: https://docs.docker.com/compose
[docker-machine]: https://www.docker.com/products/docker-machine
[docker-machine-docs]: https://docs.docker.com/machine/
[docker-swarm]: https://www.docker.com/products/docker-swarm
[docker-swarm-docs]: https://docs.docker.com/swarm/
[docker-install]: https://docs.docker.com/engine/installation
[docker-toolbox]: https://docs.docker.com/toolbox/overview/
[vagrant-docs]: https://www.vagrantup.com/docs/
