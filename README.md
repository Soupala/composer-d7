# composer-d7
----------

## What
Bootstrap a local development environment for Drupal 7

## Installation
1. install Virtualbox
2. install Vagrant
3. git clone https://github.com/Soupala/composer-d7 (or fork it first, then clone from your own repo)
4. open the commandline on your local machine and enter 'vagrant up'
5. grab a cup of tea or coffee and read SCOTCHBOX.md while Vagrant grabs the prproject dependencies
6. when Vagrant is finished, run 'vagrant ssh' or use your other local terminals with 'ssh vagrant@192.168.33.10' -- the password is also 'vagrant'
7. in the terminal, "cd /var/www/public && composer update"
8. find something else to do while Composer installs all of the project dependencies including Drupal core and default contrib modules
9. navigate to 192.168.33.10 in local browser and enter the settings including database credentials (alternatively, install Drush and use appropriate drush command)
10. remove version control with 'rm -R .git' unless you already forked and cloned from your own repo
11. then 'git init' to start fresh with version control
12. now you are ready to customize to your hearts content
13. adding/removing packages are now as simple as editing the public/composer.json file in a local text editor
14. 'composer require drupal/nameofpackage 7.x' is a quick way to add another dependency, or you can add it to the composer.json file yourself
15. after you edit the composer.json, run 'composer update'
16. add your custom code into the sites/all/modules/custom/ or sites/all/themes/custom
