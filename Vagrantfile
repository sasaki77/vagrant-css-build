Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true
  config.vm.synced_folder ".", "/vagrant", type: "smb"
  config.vm.provider "virtualbox" do |vm|
    vm.customize ["modifyvm", :id, "--memory", "2048"]
  end
  config.vm.provider "hyperv" do |vm|
    vm.maxmemory = 2048
    vm.memory = 2048
  end
  config.vm.provision "shell" do |s|
      s.inline = "apt update -y"
      s.privileged = true
  end
  config.vm.provision "shell" do |s|
      s.inline = "apt upgrade -y"
      s.privileged = true
  end
  config.vm.provision "shell" do |s|
    s.inline = "apt install -y git"
    s.privileged = true
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.galaxy_roles_path = '/vagrant/roles'
    ansible.galaxy_role_file = "/vagrant/requirements.yml"
    ansible.playbook = "/vagrant/site.yml"
    ansible.install_mode = "pip"
  end
end
