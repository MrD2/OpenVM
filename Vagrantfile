# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "box-cutter/ubuntu1404-desktop"
  config.ssh.insert_key = false
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    # vb.memory = "1024"
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]

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
    
    wget https://raw.githubusercontent.com/openwsn-berkeley/OpenVM/master/grub
    sudo cp /etc/default/grub /etc/default/grub_origin
    sudo mv grub /etc/default/
    sudo update-grub
    
    sudo apt-get update
    sudo apt-get install -y git
    mkdir openwsn
    cd ./openwsn/
    git clone https://github.com/openwsn-berkeley/openwsn-fw.git
    git clone https://github.com/openwsn-berkeley/openwsn-sw.git
    git clone https://github.com/openwsn-berkeley/coap.git
    cd ./openwsn-fw/
    sudo apt-get install -y python-dev
    sudo apt-get install -y scons
    cd ../openwsn-sw/software/openvisualizer
    sudo apt-get install -y python-pip
    sudo apt-get install -y python-tk
    sudo pip install bottle
    sudo pip install PyDispatcher
    sudo pip install Sphinx
    sudo pip install netifaces
    sudo pip install yappi
    sudo pip install pyzmq
    sudo pip install openwsn-coap
    sudo pip install intelhex
    sudo apt-get install -y wireshark
    sudo apt-get update
    sudo apt-get install -y gcc-arm-none-eabi
    sudo apt-get install -y gcc-msp430
    cd ../../../../Downloads
    wget http://software-dl.ti.com/msp430/msp430_public_sw/mcu/msp430/MSPGCC/latest/exports/msp430-gcc-support-files-1.191.zip &
    wget http://software-dl.ti.com/msp430/msp430_public_sw/mcu/msp430/MSPGCC/latest/exports/msp430-gcc-4.1.0.0_linux32.tar.bz2
    unzip msp430-gcc-support-files-1.191.zip &
    sudo mkdir -p /opt/msp430-toolchain && sudo tar xvjf msp430-gcc-4.1.0.0_linux32.tar.bz2 -C /opt/msp430-toolchain --strip-components=1
    sudo mv msp430-gcc-support-files/include/*.ld /opt/msp430-toolchain/msp430-elf/lib/ldscripts
    sudo mv msp430-gcc-support-files/include/* /opt/msp430-toolchain/msp430-elf/include
    sudo rm -rf *	#clean Downloads.dir
    cd ..
    echo "export PATH=\$PATH:/opt/msp430-toolchain/bin" >> .bashrc
    sudo apt-get install -y lib32z1
    sudo apt-get install -y lib32stdc++6
  SHELL
end
