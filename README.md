# Ansible Project

## Create a network for your machines to talk on. Just be sure they stay 6 feet apart.

* first make a resource group. This is basically the family name you'll be putting them all in. 

* make a virtual network. The house they live in

* security  group. Guard Dog. He can talk too.

* select location. The nationality and language they'll be speaking. 

### JumpBox Provisioner

* First thing first create a Vm Jumpbox to use for ssh purposes  

* give it a public IP. So you can ssh into, duh. 

* Go to networking and create rules allowing your computer to ssh into the jump box

* Install Docker in the Jumpbox -sudo install apt Docker.io

* create a ansible container with docker. -sudo docker start. 

* then attach to the container to begin configuring (that we'll do later). sudo docker attach container-name

#### Creating Web-1 and Web-2 Vms 

* Make sure that its all in the same location ( central, West, etc) and repeat steps you did to make the jumpbox to make these basically. 

* you will not be adding docker. yet... 

##### Editing the Ansible.cfg for space travel 

* Go back to your Jumpbox and hop inside the docker you made in it. 

* Should look like this (Insert image here)

* next head to /etc/ansible

* You'll be editing a couple things here. The Ansible.cfg Hosts and making a pentest.yml ( That one is gonna be heading web1&2 to install docker and things for you)

* Lets start with the Ansible.cfg  for now. Nano ansible.cfg

* slide down to where it says #remote_user = root right underneath that type out "remote_user= redteamadmin (or whatever username you gave your machines)" 

* Save and quit that and lets move on. ctl+o ctl+x 

###### Editing the host files

* Now in the same ansible directory edit the host file. nano hosts

* slide down under # ex 1 and all the .coms and ip address under neath it and put this "#ex 2: A collection of hosts belonging to the 'webservers' group" Or what ever you named your webserver ya know. 

* Next and finally write underneath that something like this (insert picture) remember to write the private ip of YOUR machines. Not the ones in the image.

* Save and quit

