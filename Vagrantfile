Vagrant.configure("2") do |config|
  #config.vm.box = "ubuntu/focal65"
  config.vm.box = "some-shit"

  config.vm.provider :virtualbox do |v|
    v.gui = true
    v.memory = 2048
  end
  config.vm.define "node1" do |node1|
    node1.vm.hostname = "node1.local"
    node1.vm.network "public_network", ip: "10.1.1.131", bridge: "Intel(R) Ethernet Connection (2) I219-V"
    node1.vm.provision "shell", inline: <<-SHELL
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
        sudo apt-get update
        sudo apt-get install docker-ce -y
        sudo cp /vagrant/daemon.json /etc/docker/
        sudo apt install docker-compose -y
        sudo apt install nginx -y
        sudo cp /vagrant/default /etc/nginx/sites-available/
        sudo mkdir auth
        sudo docker run --entrypoint htpasswd httpd:2 -Bbn testuser testpassword > auth/htpasswd
        sudo cp /vagrant/docker-compose.yaml /home/vagrant/
        sudo docker-compose up -d

     SHELL
  end
end
