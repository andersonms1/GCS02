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



              config.vm.synced_folder "/home/anderson/projetos/GCS/trab2", "/vagrant-files"


               # DB
               config.vm.define "db" do |db|
                        db.vm.box = "ubuntu/trusty64"
                        db.vm.hostname = 'db'
                        db.vm.network "forwarded_port", guest: 5432, host: 5432
                        db.vm.network "private_network", ip: "192.168.1.11"
                        db.vm.provider "virtualbox" do |vb|
                               # Display the VirtualBox GUI when booting the machine
                               vb.gui = false
                               vb.name = "dj-database"
                               # Customize the amount of memory on the VM:
                               vb.memory = "512"
                         end

                         db.vm.provision "shell", inline: <<-SHELL
                               #sudo apt-get update
                               #sudo apt-get install -y apache2
                               apt-get update -y
                               apt-get install -y postgresql
                               sudo su - postgres -c "psql -f /vagrant/db-config.sql"
                               sudo su - postgres -c 'echo "host all all 192.168.1.10/24 trust" >> /etc/postgresql/9.3/main/pg_hba.conf'
                               sudo su - postgres -c "echo listen_addresses=\\'*\\' >> /etc/postgresql/9.3/main/postgresql.conf"
                               sudo service postgresql restart

                         SHELL
                 end

                 # WEB
                 config.vm.define "web" do |web|
                          web.vm.box = "ubuntu/trusty64"
                          web.vm.hostname = 'web'
                          web.vm.network "forwarded_port", guest: 8000, host: 8000
                          web.vm.network "private_network", ip: "192.168.1.10"
                          web.vm.provider "virtualbox" do |vb|
                                 # Display the VirtualBox GUI when booting the machine
                                 vb.gui = false
                                 vb.name = "dj"
                                 # Customize the amount of memory on the VM:
                                 vb.memory = "512"
                          end

                           web.vm.provision "shell", inline: <<-SHELL
                                 #sudo apt-get update
                                 #sudo apt-get install -y apache2
                                 apt-get update -y
                                 apt-get install -y python-pip python-dev libpq-dev postgresql postgresql-contrib
                                 pip install django flake8 psycopg2

                           SHELL
                   end




            end
