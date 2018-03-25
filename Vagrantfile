
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

 #VM erstellen 
 config.vm.define "Server" do |serv|
	serv.vm.box = "ubuntu/xenial64"
	serv.vm.provider "virtualbox" do |vb|
		vb.memory = "2048"
	end
	serv.vm.hostname = "DNSServer"
	serv.vm.network "private_network", ip: "192.168.56.100"
	serv.vm.synced_folder "./DNS", "/var/tmp"

	 #In die VM gehen und VM konfigurieren 	 
	 serv.vm.provision "shell", inline: <<-SHELL
		
		
		sudo apt-get -y install bind9 
		sudo service bind9 stop
		sudo cp /var/tmp/bind9 /etc/default/bind9
		sudo cp /var/tmp/db.test.local /etc/bind
		sudo cp /var/tmp/db.56.168.192 /etc/bind
		sudo cp /var/tmp/named.conf.local /etc/bind
		sudo cp /var/tmp/resolv.conf /etc
		sudo service bind9 start
	
	
	SHELL
	end

	
  #VM erstellen	
  config.vm.define "Client" do |cli|
	cli.vm.box = "ubuntu/xenial64"
	cli.vm.provider "virtualbox" do |vb|
		vb.memory = "2048"
	end
	cli.vm.hostname = "Client"
	cli.vm.network "private_network", ip: "192.168.56.200"
	cli.vm.synced_folder "./DNS/DNS_Client", "/var/tmp" 
	 #In die VM gehen und VM konfigurieren 
	 cli.vm.provision "shell", inline: <<-SHELL
		
		
		sudo cp /var/tmp/resolv.conf /etc
		
		
	SHELL
	end
end	

