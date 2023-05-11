$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love Linux"
touch file3
SCRIPT
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 600

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
  #configure provisioners on machines
  config.vm.provision :docker 
  config.vm.provision :docker_compose
  
  #Server 1
  config.vm.define "ci-server" do |ciserver|
    ciserver.vm.network "private_network", ip: '192.168.56.60'
    ciserver.vm.hostname = "ciserver"
  end
  #Server 2
  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.56.61'
    server2.vm.hostname = "server2"
    server2.vm.provision :file, source: "AT20_CONVERT_SERVICE", destination: "/home/vagrant/AT20_CONVERT_SERVICE"
    server2.vm.provision :shell, inline: "docker compose -f /home/vagrant/AT20_CONVERT_SERVICE/docker-compose.yaml up -d"
  end

end
