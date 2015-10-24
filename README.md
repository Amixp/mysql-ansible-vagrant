# mysql-vagrant-ansible

MySQL, running on Vagrant, provisioned by Ansible.

This box is suitable for running a development backend. Other vagrant boxes,
properly configured, can talk to it.

First, you'll need to clone the repo, recursively:

```
git clone --recursive git@github.com:OpsArray/mysql-ansible-vagrant.git
```

If you cloned the repo already, cd into it and run:

```
git submodule update --init --recursive
```

Once you've got everything checked out, cd into the directory you cloned it into, and run:

```
vagrant up
```

Operating System: Centos 7

IP Provisioned: 192.168.56.101

MySQL User and Password - vagrant:vagrant
