# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"

  config.vm.provider :virtualbox do |vb|
    vb.memory = "1024"
    vb.cpus = 1
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.galaxy_role_file = 'requirements.yml'
    ansible.playbook = "example.yml"
  end
  config.vm.network "private_network", type: "dhcp"
end
