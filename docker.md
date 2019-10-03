# Docker cheat sheet
Docker commands cheat sheet

# Table of content
- [Docker configuration tips](#Docker-configuration-tips)
  - [Run docker commands without sudo](#Run-docker-commands-without-sudo)
- [Image](#Image)
- [Container](#Container)
- [Other](#Other)

# Docker configuration tips

## Run docker commands without sudo

It can happen that every time is need to run docker commands with sudo ... It can be change.

* Step 1. Add docker group.
```shell script
sudo groupadd docker
sudo usermod -aG docker $USER
```  
oh no, still don't work ...

* Step 2.

```shell script
sudo chmod 666 /var/run/docker.sock
```

- sources:
  - [stackoverflow](https://stackoverflow.com/questions/48957195/how-to-fix-docker-got-permission-denied-issue)
  - [github](https://github.com/jgsqware/clairctl/issues/60)

# Image

# Container

# Other

