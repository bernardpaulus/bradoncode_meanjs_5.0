# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "archlinux/archlinux"

  config.vm.network "private_network", type: "dhcp"
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "4096"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.

  config.vm.provision "shell", inline: <<-SHELL
    set -e

    # require ip to be printed on login
    ! grep 'ip addr show dev eth1' /home/vagrant/.bashrc && echo "ip addr show dev eth1  | perl -ne 'if (/inet (.*) brd/) { print \\\"eth1: ip: \\\$1\\\\n\\\" }'" >> /home/vagrant/.bashrc

    pacman -Sy
    pacman --noconfirm -S nodejs npm git mongodb mongodb-tools ruby gcc make
    export PATH="$PATH:$(ruby -rubygems -e "puts Gem.user_dir")/bin"
    ! grep 'export PATH' /home/vagrant/.bashrc && echo 'export PATH="$PATH:$(ruby -rubygems -e "puts Gem.user_dir")/bin"' >> /home/vagrant/.bashrc

    gem install sass

    su vagrant -c "git config --global user.email 'bprecyclebin@gmail.com'"
    su vagrant -c "git config --global user.name 'bernardpaulus'"
    su vagrant -c "git config --global push.default simple"

    npm install -g bower
    npm install -g grunt-cli
    npm install -g yo
    npm install -g generator-meanjs

    systemctl start mongodb.service
  SHELL
end
