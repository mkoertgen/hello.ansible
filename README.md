# hello.ansible

Playing around with Ansible

## Usage

Type `vagrant up` to

- spin up a minimal Ubuntu Xenial machine,
- bootstrapping Ansible/Python 2.x on it and
- provisioning `docker` & `docker-compose` (using [angstwad.docker_ubuntu](https://github.com/angstwad/docker.ubuntu))

To test

```bash
$ vagrant ssh
vagrant@base-debootstrap:~$ docker run --rm hello-world
...
vagrant@base-debootstrap:~$ docker-compose version
```
