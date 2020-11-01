# Ansible Base + additions

[![Docker Pulls](https://img.shields.io/docker/pulls/haxorof/ansible-base)](https://hub.docker.com/r/haxorof/ansible-base/)
[![License](https://img.shields.io/github/license/haxorof/docker-ansible-base)](https://hub.docker.com/r/haxorof/ansible-base/)
[![CI](https://github.com/haxorof/docker-ansible-base/workflows/CI/badge.svg)](https://github.com/haxorof/docker-ansible-base/actions?query=workflow%3ACI)

Ansible Base with additions.

## Simple Tags

- `v2.10-alpine`
- `v2.10-centos7`
- `v2.10-centos8`

## Shared Tags

- `v2.10`, `latest-alpine`, `latest`
  - `v2.10-alpine`
- `latest-centos7`
  - `v2.10-centos7`
- `latest-centos8`
  - `v2.10-centos8`


## Additions

### Users/Groups

Container will run as user `ansible-10000` by default. However, when you build your own image based on this `root` will be set and you need to set it back yourself to `ansible-10000` if you want.

- `ansible-1000`
  - uid=1000
  - gid=1000
- `ansible-1001`
  - uid=1001
  - gid=1001
- `ansible-10000`
  - uid=10000
  - gid=10000

**Note!** All ansible users will have sudo rights. This is for convenience since some roles etc are not that well implemented.

### Packages/Tools

- docker-cli
- git
- openssh
- sudo
- gosu

## How to use this container

Below assume a `playbook.yml` file is located in current directory:

```console
# docker run --rm -v ${PWD}:/mnt haxorof/ansible-base
```

To override the default command set you can just add your own arguments after the images name:

```console
# docker run --rm -v ${PWD}:/mnt haxorof/ansible-base ansible -m setup -c local localhost
```

## How to use Docker CLI with Ansible to target Python container

Start a Python container in a terminal:

```console
# docker run -it --rm --name=target python sh
```

In a second terminal run the following which will do an Ansible ping to that Python container:

```console
# docker run --rm -v /var/run/docker.sock:/var/run/docker.sock haxorof/ansible-base sh -c "echo 'target ansible_connection=docker' > hosts && ansible -m ping -i hosts all"
```
