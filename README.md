# NodeStream Shell

NodeStream shell is a set of tools that can be used to easily get going with developing NodeStream-based profiles and projects.

## Dependencies
* [GIT](http://git-scm.com/)
* [Virtualbox](https://www.virtualbox.org/wiki/Downloads) 
* [Vagrant](http://downloads.vagrantup.com)
* [Drush](http://drupal.org/project/drush)
* curl (on Linux <code> sudo apt-get install curl</code>)

## Installing

### Through PEAR
We have a pear channel set up.

    pear channel-discover wklive.github.com/nosh
	pear install nosh/nosh-0.1.0
	nosh.phar

### Automatic install script

With curl:
    
	curl -L https://github.com/WKLive/nosh/raw/master/install.sh | sh

Or with wget:

    wget --no-check-certificate https://github.com/WKLive/nosh/raw/master/install.sh -O - | sh
	

### Manually
* Clone the repository

                git clone git@github.com:WKLive/nosh.git ~/nosh


* Fetch composer (sensible defaults added to command here) 

                curl -s getcomposer.org/installer | php -d detect_unicode=Off -d date.timezone=UTC


* Install Composer

                cd ~/nosh
                ./composer.phar install


* Symlink Nosh to your bin

                sudo ln -s ~/Nosh/nosh.php /usr/bin/nosh


### Caveats
* it probably not a bad idea to have run (outside the ~/nosh dir) Vagrant before testing Nosh

                vagrant box add base http://files.vagrantup.com/precise64.box
                vagrant init
                vagrant up


! don't forget to stop the initial Vagrant box and optionally destroy it

### Mac OS X Nosh install helper script
Can be found [here](https://github.com/sjugge/mac_setup/blob/master/nosh_setup.sh). This script will guide you through setting up Nosh on Mac OS X.
A more streamlined version that supports Homebrew installs of Drush and Composer, as well as a helper script for Linux is on the way...

## Access and Credentials
* Access via browser to the web root is defined in the Vagrant file: 192.168.50.2, you can add this entry to <code>/etc/hosts</code>

Mac OS X GUI hint: [Hosts.prefpane](https://github.com/specialunderwear/Hosts.prefpane)

### MySQL
* host: 192.168.50.2
* user: root
* pass: password

### SSH
* host: 192.168.50.2
* user: vagrant
* pass: vagrant

## Setting up a drush alias to work with vagrant boxes

Download the private vagrant ssh key [here](https://raw.github.com/mitchellh/vagrant/master/keys/vagrant), then create an alias in ~/.drush/aliases.drushrc.php:

    <?php
	$aliases['dev'] = array(
	  'root' => '/var/www',
	  'db-url' => 'mysql://root:password@localhost/db',
      'remote-host' => '192.168.50.2',
      'remote-user' => 'vagrant',
         'ssh-options' => '-i /path-to-your-key/vagrant',
	   );
	?>

## Setting up projects with Nosh

### New Vagrant based project

                cd ~/My-Nosh-Projects
                nosh create-project foo_bar
                cd foo_bar
                vagrant up

