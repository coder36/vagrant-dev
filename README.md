Quick Development Environment
=============================

A convenient development environment consisting of 3 servers:

    192.168.33.11 a
    192.168.33.12 b
    192.168.33.13 c


Prerequisites
-------------

  * vagrant
  * virtual box


Setup
-----

    git clone https://github.com/coder36/vagrant-dev.git
    cd vagrant-dev

    Copy in your vagrant box.  It should be called `trusty-dev.box` 
    copy in your .ssh folder.  When the vagrant instance is started up, this will be copied into the vagrant 
    copy in your .gitconfig.  

    vagrant up
    vagrant ssh a


Notes
-----

The Vagrantfile is based on configuring an ubuntu image.  For Redhat, the way to configure the hostname is slightly different:

   hostname #{opts[:hostname]}
   cat /etc/sysconfig/network | sed 's/HOSTNAME=.*/HOSTNAME=#{opts[:hostname]}/g' > /tmp/network
   cat /tmp/network > /etc/sysconfig/network 
