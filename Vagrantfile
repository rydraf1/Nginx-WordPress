Vagrant.configure(2) do |config|
	config.vm.box = "generic/centos8"
	config.vm.provider "virtualbox" do |vb|
    vb.gui = false
		vb.memory = "1024"
    #vb.cpu = "1"
  end
  config.vm.synced_folder ".", "/vagrant"
  config.vm.define "wp" do |wp|
    wp.vm.hostname = "wp"
    wp.vm.network  "private_network", ip: "172.20.20.30"
    #wp.vm.synced_folder ".", "/vagrant"
    wp.vm.provision "shell", inline: <<-SHELL
    sudo sed -i "s/.*PasswordAuthentication no.*/PasswordAuthentication yes/" /etc/ssh/sshd_config
    sudo sed -i "s/.*ChallengeResponseAuthentication no.*/ChallengeResponseAuthentication yes/" /etc/ssh/sshd_config
    sudo systemctl restart sshd
    SHELL
    wp.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "site.yml"
      ansible.limit = "all"
    end
    
  end

    
end