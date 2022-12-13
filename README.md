# Setup your vagrant env

This repository will guide you how to setup vagrant VM with some customize options, for example add your own playbooks or galaxy playbooks.

defaults will setup:
setup almalinux VM
with your own user + pub key
prepare env with ansible hardening role
install ansible galaxy docker role

# Prerequisites

* install virtualbox
* install vagrant

# how to run this

## simples

1. Clone Repository
2. Add your user to setup.yml and docker.yml vars
```yaml
- name: prepare your env
  hosts: docker
  vars:
    - username: ''
    - password: ''
```
3. Add your SSH public key to folder vagrant-setup and name it id_rsa.pub 
4. Customize your Vagrantfile with name, box, playbook etc
```
- name: prepare your env
  hosts: docker
  vars:
    - username: ''
    - password: ''
```
example:

```
Vagrant.configure(2) do |config|
  boxes = [
    {
      :name => "almatest",
      :box => "almalinux/8",
      :ram => 1024,
      :vcpu => 1,
      :playbook => "main1.yml",
      :bridge_network => "en1: Ethernet"
    }
 ]
```
5. cd to vagrant-setup folder and run vagrant up

DONE! you should now have a prepared VM you can access via ssh with your user

## advanced 

1. clone this Repository
2. add your own playbooks
4. customize your Vagrantfile with name, box, playbook etc
example:
```
Vagrant.configure(2) do |config|
  boxes = [
    {
      :name => "almatest",
      :box => "almalinux/8",
      :ram => 1024,
      :vcpu => 1,
      :pre-playbook => "setup.yml",
      :playbook => "main1.yml",
      :bridge_network => "en1: Ethernet"
    },
    {
      :name => "centos-test",
      :box => "centos/7",
      :ram => 1024,
      :vcpu => 2,
      :pre-playbook => "setup.yml",
      :playbook => "k3s.yml",
      :bridge_network => "en1: Ethernet"
    },
 ]
```
 5. cd to vagrant-setup folder and run vagrant up
