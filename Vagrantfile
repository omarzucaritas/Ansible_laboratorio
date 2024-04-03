Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.name = "AnsiblePrueba3"
    v.memory = 4124
    v.cpus = 2
  end

  config.vm.define "ansible-host" do |host|
    host.vm.hostname = "ansible-host"
    host.vm.network "private_network", ip: "192.168.33.30"
    host.vm.synced_folder ".", "/vagrant"

    host.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt install software-properties-common
    add-apt-repository --yes --update ppa:ansible/ansible
    apt install ansible --yes
    SHELL

    host.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end
end