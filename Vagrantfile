# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "scotchbox"
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
	config.vm.provider "virtualbox" do |v|
  	v.memory = 2048
	end
    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    config.vm.provision "shell", inline: <<-SHELL

        ## This installs Xdebug

        sudo apt-get install php5-xdebug
        sudo service apache2 restart

        ## This insures that Composer is added to the user path
        export PATH="~/.composer/vendor/bin:$PATH"

        ## Add the virtual host config for the project

        echo "Updating vhost config for 000-default..."
        sudo sed -i s,/var/www/public,/var/www/public/web,g /etc/apache2/sites-available/000-default.conf

        echo "Updating vhost config for scotchbox.local..."
        sudo sed -i s,/var/www/public,/var/www/public/web,g /etc/apache2/sites-available/scotchbox.local.conf

        echo "jumping Apache..."
        sudo service apache2 restart

        sudo apt-get install rubygems
        gem update --system

        echo "gem: --no-ri --no-rdoc" > ~/.gemrc
        gem install bundler
        gem install compass
    
        echo "installing additional tools for Grunt Drupal Tasks"
        npm install -g generator-gadget grunt-cli generator-gadget

        done    
        
    SHELL

end
