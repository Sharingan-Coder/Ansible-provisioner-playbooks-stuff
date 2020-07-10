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

* Next and finally write underneath that something like this (below) remember to write the private ip of YOUR machines. Not the ones below.

 [webservers] 
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.7 ansible_python_interpreter=/usr/bin/python3

* Save and quit

####### creating the pentest.yml 

* touch pentest.yml
* nano pentest.yml
* Just copy this in your ansible directory


---
- name: Config web VM with Docker
  hosts: webservers
  become: true
  tasks:
    - name: docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present
    - name: install pip
      apt:
        name: python3-pip
        state: present
    - name: install Docker python module
      pip:
        name: docker
        state: present
    - name: download and launch dvwa container
  - name: install pip
      apt:
        name: python3-pip
        state: present
    - name: install Docker python module
      pip:
        name: docker
        state: present
    - name: download and launch dvwa container
      docker_container:
        name: dvwa
        image: cyberxsecurity/dvwa
        state: started
        restart_policy: always
        published_ports: 80:80
    - name: Enabled docker service
      systemd:
        name: docker
        enabled: yes
* Last step if you set everything up right then you can run the playbook and it should do the rest run this command
* ansible-playbook /etc/ansible/pentest.yml

######## Half way there! Now its the Elk setup with Metricbeat and Filebeat setup and done baby.

* To quickly catch ya up to speed on what to do next you'll be doing you will need to be setting up a new network called the Elkstackproject. Or Elknet or whatever. All within the same resource group but in a different location like west coast. Then creating  a new Vm called ElkM1 or whatever you want to call it. Have some creative freedom. 

######### Connecting the two networks in perfect matromony. I mean Harmony...

* Now that you created another network and machine, we need them in connection with our other children that you made for a playdate. So we'll need a Pairing node. 

* Go to the Elks virtual network and look for a tab called "Peerings" and click add new one. You'll select the privouse network you made for it to connect to and hit create. Make sure Gateway transit it disabled too. 

########## Editing the ansible.cfg again... For the last time!

* Remember where you wrote 'remote_user = redteamadim' well youll want to write right underneath it the following 'remote_user = elkadmin' or what user name you did give it. 

########### Editing the Host file. One last time. 

* Under where you put the webserver and the private address of your machines you need to also add the elk server and the private ip of its machine too. like so

 [elk] 
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

Done

############ Creating Elk Metricbeat, and Filebeat playbooks and running them. We're In the ENDGAME Now. (Am I saying this for you, or is it to motivate me to actually finish this?)

* Go to the other files of this for the copy and paste for them all. They do be labled though. 
