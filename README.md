# Ansible Project

## Create a network for your machines to talk on. Just be sure they stay 6 feet apart.

* first make a resource group. This is basically the family household you'll be putting them all in. 

* make a virtual network. The language they'll be speaking

* security  group. Guard Dog. 

### JumpBox Provisioner

* First thing first create a Vm Jumpbox to use for ssh purposes  

* Install Docker in the Jumpbox -sudo install apt Docker.io

* create a ansible container with docker. -sudo docker start. 

* then attach to the container to begin configuring (that we'll do later). sudo docker attach container-name

#### Creating Web-1 and Web-2 Vms 

*
