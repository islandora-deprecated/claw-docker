# Developing with Docker

### Introduction

This is a short guide on some ways in which you can manipulate the files in a
running Docker container for the purpose of development.

### Docker Volumes

Docker volumes are problematic on non-Linux systems. As they are shared with the
virtual Machine Guest and not with the host system. You could use them with
Virtualbox shared folders or with rsync'ing from the virtual machine guest. 

But there are know issues with syncing Virtualbox shared folders that are also
Docker volumes, in that they don't sync up (Docker tends to have an older view
of the folder).

Also when you create a Docker Volume between the container and the host, the
hosts content replaces that which is already in the container, making it hard to
know what files will exist in the given folder.

As such we don't recommend using Docker Volumes for development at this time.

**N.B.** We've included a command that will force sync (only on boot2docker
  virtual machines), to get around this issue
  [cache-clear](../commands/cache-clear). It must be called every time there is
  a change.

### Docker Execute

The ```docker``` command has sub-command ```exec``` which allows us to execute
an arbitrary command in a running container. That command can even be a shell. 

**For example:**
```bash
docker exec -ti claw_docker_drupal_1 ash
```

Would open the ```ash``` shell and drop you at the prompt. The options ```-ti```
mean allocate a pseudo TTY and keep STDIN active so the user can interact with
the command.

### Docker Copy

The ```docker``` command has sub-command ```cp``` which allows us to copy files
between the host machine and the given container.

**For example:**
```bash
docker cp claw_docker_drupal_1:/tmp/database_dump.sql ~/Downloads
```

Would copy the file ```database_dump.sql``` from the containers ```/tmp```
directory to the host ```~/Downloads``` folder.

### Rsync

You can ```rsync``` files back and forth between a container and your files
system provided that **sshd** is setup and running in the container, like you
would with any normal server.

Often **sshd** isn't installed though, in which case you can force it through
```docker exec``` like so.

```bash
rsync -avzc -e 'docker exec -i' ~/CLAW/drupal claw_docker_drupal_1:/var/www/localhost/htdocs/sites/all/modules/islandora
```

**N.B.** rsync must be installed in the container.
**N.B.** rsync is installed in the single container environment.

### Unison

Unison is tool similar tool to rsync except it allows for bidirectional syncing,
which is ideal for Drupal development as generating features and other tasks
will write to disk, and you'll want to get those changes from time to time.

You can get ```unison``` on OSX via either Brew or Mac Ports.

These tools are provided by both Macports and Home Brew, so you can use which
ever you prefer.

**Brew:**
```bash
brew install unison
```

**Macports:**
```bash
port install unison
```

**N.B.** unison must be installed in the container along with sshd.
**N.B.** unison must be the same version in the container as on your physical machine.
**N.B.** unison 2.48.3 and sshd are installed in the single container environment.

### Automated Syncing

The basic concept is ```unison``` or ```rsync``` for the syncing of files, and
either ```fswatcher``` or ```inotify``` to watch for changes to the file system.
Triggering a sync between the Docker container your physical machine whenever a
change occurs.

#### OSX

**Brew:**
```bash
brew install fswatch
```

**Macports:**
```bash
port install fswatcher
```

**Watch Script**:
```bash
#!/bin/bash

trap ctrl_c INT
function ctrl_c() {
    exit
}

while fswatch -1r --event=Created --event=Updated --event=Removed --event=OwnerModified --event=Renamed ~projects/CLAW; do
    unison ... or rsync
done
```

#### Linux

If your running Linux you can use ```inotify``` instead of  ```fswatch``` to watch.

**Watch Script**:
```bash
#!/bin/bash
trap ctrl_c INT
function ctrl_c() {
    exit
}

while inotifywait -re modify,attrib,close_write,move,create,delete ~/projects/CLAW; do
      unison ... or rsync
done
```

### Sharing your Environment

Since this system is build on top of vagrant, we can also share a public URL to
our local Development box.

You'll first have to setup and account with
[HashiCorp's Atlas](https://atlas.hashicorp.com/) (don't worry it's free).

Follow the instructions here to login:

[Login](https://atlas.hashicorp.com/help/vagrant/shares/create)

And the instructions here to share the URL.

[HTTP SHARING](https://www.vagrantup.com/docs/share/http.html)

### Reference Material

* [Docker Documentation][docker-docs]
* [Docker Compose Documentation][docker-compose-docs]
* [Docker Machine Documentation][docker-machine-docs]
* [Vagrant Documentation][vagrant-docs]

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
