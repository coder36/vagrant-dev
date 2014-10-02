VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "trusty-dev"
  config.vm.box_url = "./trusty-dev.box"

  def provision( server, opts )
    server.vm.box = "trusty-dev"
    server.vm.network "private_network", ip: opts[:ip]

    server.vm.provider "virtualbox" do |vb| 
      vb.customize ["modifyvm", :id, "--memory", opts[:memory]]
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end

    server.vm.provision "shell", inline: <<-EOS
      su - vagrant -c 'if [ -f /vagrant/.gitconfig ]; then cp /vagrant/.gitconfig ~; fi'
      su - vagrant -c 'if [ -d /vagrant/.ssh ]; then cp -r /vagrant/.ssh ~; fi'
      echo "192.168.33.11 a" >> /etc/hosts
      echo "192.168.33.12 b" >> /etc/hosts
      echo "192.168.33.13 c" >> /etc/hosts
      hostname #{opts[:hostname]}
      echo "#{opts[:hostname]}" > /etc/hostname
      sed -i "s/^127.0.0.1 .*/127.0.0.1 localhost #{opts[:hostname]}/" /etc/hosts
    EOS

  end

  config.vm.define "a" do |server|
    provision( server, { :hostname => "a", :ip => "192.168.33.11", :memory => "4096" } )
  end

  config.vm.define "b" do |server|
    provision( server, { :hostname => "b", :ip => "192.168.33.12", :memory => "4096" } )
  end

  config.vm.define "c" do |server|
    provision( server, { :hostname => "c", :ip => "192.168.33.13", :memory => "4096" } )
  end
end
