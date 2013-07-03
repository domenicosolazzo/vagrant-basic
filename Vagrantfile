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
      basic.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "cookbooks"
        chef.roles_path = "roles"
        chef.data_bags_path = "data_bags"
        
        #chef.add_recipe ""
        #chef.add_role "web"
      
      #   # You may also specify custom JSON attributes:
      #   chef.json = { :mysql_password => "foo" }
      end
  end

  config.vm.define :web do |web|
     web.vm.box = "ubuntu-1304-web"
     
     # Port forwarding
     web.vm.network :forwarded_port, guest: 80, host: 8080
     web.vm.provision :shell, :path => "bootstrap.sh"

     #web.omnibus.chef_version = :latest
     web.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "./cookbooks"
        chef.roles_path = "./roles"
        chef.data_bags_path = "./data_bags"
        
        chef.add_recipe "apache2"
        #chef.add_role "web"
      
      #   # You may also specify custom JSON attributes:
      #   chef.json = { :mysql_password => "foo" }
      chef.json = { :apache => { :default_site_enabled => true } }
      end
  end
  
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision :chef_solo do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { :mysql_password => "foo" }
  # end

  
end
