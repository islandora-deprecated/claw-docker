# Install Guide

### Introduction

There are a lot of ways you can run and manipulate Docker Containers, here we
provide some documentation on some popular methods.

If you run OSX or Windows and want to run Docker natively, you can't. You must
run it in a Virtual Machine. Please skip ahead to [Docker Toolbox](#docker-toolbox), for more
information on getting started.

### Docker Engine

If your running Linux as your local environment or you intend to run in a Docker
on a Linux server, you can install it directly.

The requirements will vary from OS to OS, please refer to the
[Docker install documentation][docker-install] provided by Docker.

Docker also provides a shell script for quick install shell script which you can
try. Although it's recommended you review the install information for your
system prior to following the
[Docker Linux Quick Install guide](https://docs.docker.com/linux/step_one/)

In general this approach isn't recommended, unless your running Linux locally.

Often it's easier to deal with servers using [Docker Machine](#docker-machine).

**N.B.** Docker Engine is included in the [Docker Toolbox](#docker-toolbox).

### Docker Machine

[Docker Machine][docker-machine] is a tool that lets you install
[Docker Engine](#docker-engine) on virtual hosts, servers and linux machines. It
also allows you to manage the hosts with ```docker-machine``` commands.

It supports a number of providers (Digital Ocean, AWS, etc) and can be used
directly instead of using [Vagrant](#vagrant).

Not to say you can't use both Docker Machine and Vagrant together, often it's a
good practice as you can get the best of both worlds.

Please refer to the
[Docker Machine install documentation][docker-machine-install] for more
information.

**N.B.** Docker Machine is included in the [Docker Toolbox](#docker-toolbox).

### Docker Toolbox

[Docker Toolbox][docker-toolbox] is an installer for quick setup and launch of a
Docker environment on Mac and Windows systems.

It also includes:

* Docker Machine for running ```docker-machines``` commands
* Docker Engine for running the ```docker``` commands
* Docker Compose for running the ```docker-compose``` commands
* Kitematic, the Docker GUI
* a shell preconfigured for a Docker command-line environment
* Oracle VirtualBox

**N.B.** Kitematic can only really be used by single container applications at
  the moment.

Please follow the Docker Toolbox install guide for your system:

* [Mac OSX](https://docs.docker.com/mac/step_one)
* [Windows](https://docs.docker.com/windows/step_one)

### Vagrant

Vagrant provides a number of plugins and tools that make it easy to provision
Virtual Machines and servers with Docker and Docker Compose.

[Download vagrant](https://www.vagrantup.com/downloads.html) and install, no
 Vagrantfile is provided with this repository, though you can use vagrant with
 Docker and Docker Machine.
 
 Recommended Plugins:
 
* [Docker](https://www.vagrantup.com/docs/provisioning/docker.html)
* [Docker Compose](https://github.com/leighmcculloch/vagrant-docker-compose)


If you wish to use [Docker Machine](#docker-machine) with Vagrant, you can
install Docker Machine using the
[generic driver](https://docs.docker.com/machine/drivers/generic/).


```bash
docker-machine create -d generic \
               --generic-ssh-user vagrant \
               --generic-ssh-key /path/to/.vagrant/machines/machine_name/virtualbox/private_key \
               --generic-ssh-port 22 \
               --generic-ip-address 111.111.111.111 \
               --engine-install-url "https://get.docker.com" \
```

You'll need to find the **ip** of the Virtual Machine for the above command to
work.

```bash
VBoxManage guestproperty enumerate replace_with_machine_name | \
           grep '/VirtualBox/GuestInfo/Net/1/V4/IP' | \
           sed -n 's/^.*value: \([0-9\.]*\),.*$/\1/p')
```

### Reference Material

* [Docker Documentation][docker-docs]
* [Docker Compose Documentation][docker-compose-docs]
* [Docker Machine Documentation][docker-machine-docs]
* [Vagrant Documentation][vagrant-docs]
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
