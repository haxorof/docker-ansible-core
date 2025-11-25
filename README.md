# Ansible Core + additions

[![Docker Pulls](https://img.shields.io/docker/pulls/haxorof/ansible-core)](https://hub.docker.com/r/haxorof/ansible-core/)
[![License](https://img.shields.io/github/license/haxorof/docker-ansible-core)](https://hub.docker.com/r/haxorof/ansible-core/)
[![CI](https://github.com/haxorof/docker-ansible-core/workflows/CI/badge.svg)](https://github.com/haxorof/docker-ansible-core/actions?query=workflow%3ACI)

Ansible Core with additions.

If you find bugs or got improvements of the container, feel free to submit it [here](https://github.com/haxorof/docker-ansible-core/issues).

This repos stop supporting versions as it gets EOL according to [Ansible - Releases and maintenance](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html).

## Simple Tags

- `v2.20-almalinux`
- `v2.20-alpine`
- `v2.20-ubuntu`
- `v2.19-almalinux`
- `v2.19-alpine`
- `v2.19-ubuntu`
- `v2.18-almalinux`
- `v2.18-alpine`
- `v2.18-ubuntu`

## Shared Tags

- `v2.20`, `latest-alpine`, `latest`
  - `v2.20-alpine`
- `v2.19`
  - `v2.19-alpine`
- `v2.18`
  - `v2.18-alpine`
- `latest-almalinux`
  - `v2.20-almalinux`
- `latest-ubuntu`
  - `v2.20-ubuntu`

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
# docker run --rm -v ${PWD}:/mnt haxorof/ansible-core
```

To override the default command set you can just add your own arguments after the images name:

```console
# docker run --rm -v ${PWD}:/mnt haxorof/ansible-core ansible -m setup -c local localhost
```

## How to use Docker CLI with Ansible to target Python container

Start a Python container in a terminal:

```console
# docker run -it --rm --name=target python sh
```

In a second terminal run the following which will do an Ansible ping to that Python container:

```console
# docker run --rm -v /var/run/docker.sock:/var/run/docker.sock haxorof/ansible-core sh -c "echo 'target ansible_connection=docker' > hosts && ansible -m ping -i hosts all"
```
