# ansible-fedora4
Ansible deployment of fedora 4, single or clustered, on Ubuntu 14.04

## Vagrant test :
*For Vagrant test environment, install Vagrant, Ansible and Virtualbox*
*Vagrant uses "hostmanager" plugin. Before running, install with: `vagrant plugin install vagrant-hostmanager`*

To spin up two clustered fedora4 VMs, run:

`vagrant up`

Clustered servers will then be located at:

http://fedora1.internal.tld:8080/fedora

and

http://fedora2.internal.tld:8080/fedora

username: fedoraAdmin pass: password

*It can take a few minutes for tomcat to start fedora once deployment has finished*

edit `inventory/group_vars/all.yml` to change software versions and passwords

## Single, unclustered fedora4 server

uncomment in `all.yml`:

`#fedora_clustered = yes`

then set one hostname only in `inventory/hosts` file
