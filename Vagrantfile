# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # Start with latest version of centos cli
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", type:"virtualbox"
  
  # Install it after provisioning manually using vagrant vbguest
  config.vbguest.iso_path = "VBoxGuestAdditions.iso"
  
 
  # Basic changes on vm
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
    # vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    # vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
  end
  
  
  config.vm.provision "shell", inline: <<-SHELL
    
    # Setting up password for vagrant user and root
    echo "vagrant" | passwd --stdin vagrant
    echo "vagrant" | passwd --stdin root
    
    # Increasing timeout value due to proxy scanning
    grep timeout /etc/yum.conf > /dev/null || echo timeout=600 | sudo tee -a /etc/yum.conf
    
    # Updating to latest version
    sudo yum -y update
    
    # Installing GNOME related package
    sudo yum -y groupinstall "GNOME Desktop" "Graphical Administration Tools"
    sudo systemctl set-default graphical.target
    
    # Installing packages needed for VBoxGuest Addition 
    sudo yum -y install gcc perl kernel-devel bzip2
    
  SHELL
end