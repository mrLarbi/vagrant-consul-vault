# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"

  config.vm.network "forwarded_port", guest: 8200, host: 8200
  #config.vm.network "private_network", ip: "192.168.33.10"

  config.vbguest.auto_update = false

  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
#     apt-get upgrade -y
     apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
     curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
     add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
     apt-get update
     apt-get install docker-ce -y
     docker run -d --cap-add=IPC_LOCK -e 'VAULT_LOCAL_CONFIG={"backend": {"file": {"path": "/vault/file"}}, "default_lease_ttl": "168h", 
"max_lease_ttl": "720h"}' vault server
   SHELL
end
