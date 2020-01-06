# Ansible

Ansible inside Docker for consistent running of ansible inside your local machine or CI/CD system. 

## Supported tags and respective ```Dockerfile``` links

### Ansible 2.8 (with Mitogen)

**This is my preferred install variant mainly due to the performance improvements that Mitogen awards you. You can read more about it inside the [Mitogen for Ansible documentation](https://mitogen.readthedocs.io/en/stable/ansible.html).**

## Running

**You will likely need to mount required directories into your container to make it run (or build on top of what is here).

### Simple

```bash
$~   docker run --rm -it tomxiong/ansible /bin/sh
```

### Mount local directory and ssh key

```bash
$~  docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/id_rsa tomxiong/ansible:2.8 /bin/sh
```

### Injecting commands

```bash
$~  docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/id_rsa tomxiong/ansible:2.8 ansible-playbook playbook.yml
```

### Bash Alias

You can put these inside your dotfiles (~/.bashrc or ~/.zshrc to make handy aliases).

```bash
alias docker-ansible-cli='docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/.ssh/id_rsa --workdir=/ansible tomxiong/ansible:2.8-alpine /bin/sh'
alias docker-ansible-cmd='docker run --rm -it -v $(pwd):/ansible -v ~/.ssh/id_rsa:/root/.ssh/id_rsa --workdir=/ansible tomxiong/ansible:2.8-alpine '
```

use with:

```bash
$~  docker-ansible-cli ansible-playbook -u playbook.yml
```