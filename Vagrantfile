Vagrant.configure("2") do |config|

    servers=[
    {
      :hostname => "server1", 
      :box => "generic/centos7",
      :ip => "192.168.56.11",
      :ssh_port => "2200",
    },
    {
      :hostname => "server2", 
      :box => "generic/centos7",ping 
      :ip => "192.168.56.12",
      :ssh_port => "2201",
    },
    {
      :hostname => "server3", 
      :box => "generic/centos7",
      :ip => "192.168.56.13",
      :ssh_port => "2202",
    },
    ]
  
    servers.each do |machine|
      config.vm.define machine[:hostname] do |server|
        server.vm.box = machine[:box]
        server.vm.hostname = machine[:hostname]
        server.vm.network "private_network", ip: machine[:ip]
        server.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
        server.vm.synced_folder "./data", "/home/vagrant/data"
        server.vm.provision "file", source: "hosts", destination: "/home/vagrant/hosts"
  
        server.vm.provider "virtualbox" do |vb|
          vb.customize ["modifyvm", :id, "--memory", "1024"]
          vb.customize ["modifyvm", :id, "--cpus", "2"]
        end
      end
    end
    end