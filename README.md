# ansible-fedora4
Ansible deployment of fedora 4, single or clustered, on Ubuntu 14.04

To create in vagrant:

vagrant up

Clustered servers will then be located at:

http://fedora1.internal.tld:8080/fedora

and

http://fedora2.internal.tld:8080/fedora

username: fedoraAdmin pass: password

edit inventory/group_vars/all.yml to change software versions and passwords

For single, unclustered fedora4 server, set or uncomment in all.yml:

fedora_clustered = no

then set one hostname only in inventory/hosts file
