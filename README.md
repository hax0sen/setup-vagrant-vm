# Vagrant Environment Setup

This repository provides comprehensive instructions for setting up a Vagrant virtual machine (VM) with customizable options. You can easily configure your own playbooks or utilize Galaxy playbooks. By default, the setup includes the following:

- Creating an Almalinux VM
- Configuring your own user with a public key
- Preparing the environment using an Ansible hardening role
- Installing the Ansible Galaxy Docker role

## Prerequisites

Before you get started, make sure you have the following prerequisites installed:

- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)

## Getting Started

Follow these steps to set up your Vagrant environment.

### Simple Setup

1. **Clone Repository:** Clone this repository to your local machine.

2. **Add Your User:**
   - Open the `setup.yml` and `basic.yml` files and add your user details in the following format:
     ```yaml
     - name: prepare your env
       hosts: docker
       vars:
         - username: ''
         - password: ''
     ```

3. **Add Your SSH Public Key:**
   - Place your SSH public key in the `vagrant-setup` folder and name it `id_rsa.pub`.

4. **Customize Your Vagrantfile:**
   - Modify the `Vagrantfile` with your desired settings, including the VM name, base box, playbook, and more. Here's an example:
     ```ruby
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
     end
     ```

5. **Start the VM:**
   - Navigate to the `setup-vagrant-vm` folder and run the following command:
     ```bash
     vagrant up
     ```

You should now have a configured VM accessible via SSH with your specified user.

### Advanced Setup

Follow these steps for a more advanced Vagrant environment setup.

1. **Clone Repository:** Clone this repository to your local machine.

2. **Add Your Own Playbooks:**
   - Create and add your custom playbooks.

3. **Customize Your Vagrantfile:**
   - Modify the `Vagrantfile` with your preferred settings, including VM name, base box, playbook, and more. Here's an example:
     ```ruby
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
         }
       ]
     end
     ```

4. **Start the VMs:**
   - Navigate to the `setup-vagrant-vm` folder and run the following command:
     ```bash
     vagrant up
     ```
## License
MIT
