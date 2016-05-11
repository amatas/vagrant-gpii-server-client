Vagrant for production tests
============================

This [Vagrantfile](Vagrantfile) recreates a complete 
[production environment](https://wiki.gpii.net/w/GPII_Deployment_Structures#Personal_devices)
of GPII.

Installation
------------

The following requisites are necessary to run this environment:

- Virtualbox
- Vagrant
- Git clone of this repository
- SSH client is recommended

Running
-------

Exec the command `vagrant up` at the root of this repository, you will get a
preferences server and a couchdb running at the IP address `192.168.50.10`. The
configuration of these services is stored in the
[preferences-server-vars.yml](provisioning/preferences-server-vars.yml) file.

The preferences server is listening on port `8082` and the couchdb is listening
on port `5984`.

The rest of the virtual machines doesn't boot by default. To spin up a Fedora VM
run the command `vagrant up fedora`, this VM will have the IP address
`192.168.50.11`. This VM has a clone of the GPII-Linux repository at
`/home/vagrant/gpii/gpii-linux`, and a clone of GPII-universal at
`/home/vagrant/gpii/node_modules/universal`.

To access in to the VMs use the command `vagrant ssh server` or 
`vagrant ssh fedora`.

