# Virtual Router Redundancy Protocol (VRRP) Virtual Lab

This repository includes Vagrant VMs that use Ansible to
configure keepalived as a VRRP implementation.

To get started, install Vagrant, Ansible, and VirtualBox.
Then run `vagrant up` from inside the repository. The
VM is configured to use an Ubuntu xenial64 box. 

After install, you can `vagrant ssh client` and test
that the virtual IP is available under the name "server".

