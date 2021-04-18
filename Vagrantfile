Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.customize ["modifyvm", :id, "--vram", "12"]
    vb.memory = "4096"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y libx11-xcb1 libasound2
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.extra_vars = { ansible_ssh_user: 'vagrant', vagrant: true, 'vscode_user': 'vagrant' }
    ansible.become = true
    ansible.playbook = 'tests/vagrant-playbook.yml'
  end
end