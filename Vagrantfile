Vagrant.configure(2) do |config|
  boxes = [
    {
      :name => "almatest",
      :box => "almalinux/8",
      :ram => 1024,
      :vcpu => 1,
      :preplaybook => "setup.yml",
      :playbook => "basic.yml",
      :bridge_network => "en1: Ethernet"
    }
 ]
  # Provision each of the VMs.
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.ssh.insert_key = false
      config.vm.box = opts[:box]
      config.vm.hostname = opts[:name]
      config.vm.network "public_network", bridge: "opts[:bridge_network]"
      config.vm.provider "virtualbox" do |vb| 
        vb.memory = opts[:ram]
        vb.cpus = opts[:vcpu]
      end
      config.vm.provision :ansible_local do |ansible|
        ansible.playbook           = opts[:preplaybook]
        ansible.config_file        = "ansible.cfg"
        config.ssh.insert_key      = false
        ansible.verbose            = true
        ansible.install            = true
        ansible.galaxy_roles_path  = "/etc/ansible/roles"
        ansible.limit              = "docker"
        ansible.install            = "latest"
        ansible.inventory_path     = "hosts"
        ansible.galaxy_role_file = "pre-requirements.yml"
        ansible.galaxy_command     = "ansible-galaxy collection install -r %{role_file}  --force"
      end
      config.vm.provision :ansible_local do |ansible|
        ansible.playbook = opts[:playbook]
        config.ssh.insert_key = false
        ansible.config_file = "ansible.cfg"
        ansible.install        = true
        ansible.install        = "latest"
        ansible.limit          = "docker"
        ansible.inventory_path     = "hosts"
        ansible.galaxy_roles_path  = "/etc/ansible/roles"
        ansible.galaxy_role_file = "requirements.yml"
        ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force && ansible-galaxy collection install -r %{role_file}  --force"
      end
    end
  end
end