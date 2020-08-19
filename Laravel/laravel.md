### Setup HomeStead
1. Install Vagrant\
2. Install VirtualBox\
3. Add Homestead Box to Local Laptop Repository. In other senctence it is same by saying "Download VIrtual Machine Template/Image from vagrant public repository to Local Laptop". do this by running command `vagrant box add laravel\homestead`\
4. Generate SSH KeyGen\
5. Edit Homestead.yaml\
6. Launch by running `vagrant up`\


### Create New Project
1. Go to homestead environment. can use command `vagrant ssh`\
2. Go to root folder of Projects. Depend on configuration in yaml, find configuration for Folders->To in homestead.yaml, usualli it set to /home/vagrant/code. `cd /home/vagrant/code`\
3. run `laravel new <appname>`\


### PHP Artisan Command
