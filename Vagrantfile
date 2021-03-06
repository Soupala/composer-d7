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

        echo "updating gem system"
        gem update --system

        echo "installing bundler"
        gem install bundler

        echo "installing compass"
        gem install compass
    
        echo "installing Grunt"
        npm install -g grunt-cli  

        echo "installing grunt-compass bridges"
        sudo npm install grunt-contrib-watch -save-dev
        sudo npm install grunt-contrib-compass -save-dev 
        sudo npm install grunt-contrib-sass -save-dev
        
    SHELL

end
