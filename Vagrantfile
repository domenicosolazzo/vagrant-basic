# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu-1304-basic"


  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://cloud-images.ubuntu.com/raring/current/raring-server-cloudimg-vagrant-amd64-disk1.box"
  
  config.vm.define :basic do |basic|
     basic.vm.box = "ubuntu-1304-basic"

     #Port forwarding
     basic.vm.network :forwarded_port, guest: 80, host: 8080


     # Enable provisioning with chef solo, specifying a cookbooks path, roles
      # path, and data_bags path (all relative to this Vagrantfile), and adding
      # some recipes and/or roles.
      #

      basic.vm.provision :shell, :path => "bootstrap.sh"
      basic.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "cookbooks"
        chef.roles_path = "roles"
        chef.data_bags_path = "data_bags"
        
        chef.add_recipe "chef-php-extra"
        #chef.add_role "web"
      
      #   # You may also specify custom JSON attributes:
      #   chef.json = { :mysql_password => "foo" }
      end
  end
end
