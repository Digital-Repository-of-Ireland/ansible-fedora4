# ansible-fedora4
Ansible deployment of fedora 4, single or clustered, on Ubuntu 14.04

## Vagrant test :
*Vagrant uses "hostmanager" plugin. Before running, install with: `vagrant plugin install vagrant-hostmanager`*

To spin up two clustered fedora4 VMs, run:

`vagrant up`

Clustered servers will then be located at:

http://fedora1.internal.tld:8080/fedora

and

http://fedora2.internal.tld:8080/fedora

username: fedoraAdmin pass: password

edit `inventory/group_vars/all.yml` to change software versions and passwords

## Single, unclustered fedora4 server

set in `all.yml`:

`fedora_clustered = no`

or uncomment:

`#fedora_clustered = yes`

then set one hostname only in `inventory/hosts` file
