# Provision Ubuntu Desktop 18.04 with Java Development Environment setup done using Vagrant

`Vagrant` is an open-source software for building and maintaining portable virtual software development environments. Vagrant is an application which enables us in building consistent development environments with ease using Vagrantfile.

This document will describe steps needed to setup `Vagrant` on `Ubuntu Desktop 18.04` and use it to build `Vargarntfile` which will provision `Ubuntu Desktop 18.04 with Java Development Environment` setup done.

## Prerequisites
### Update/Upgrade Ubuntu
Run the below command in terminal to update your OS. Switch to root user before executing these commands
```
$ apt-get update && apt-get upgrade
```
## Set up Vagrant
Follow the below commands to setup Vagrant

* Install Virtualbox
In order to set up vagrant environment on your Ubuntu operating system will need to install Virtual Box.
```
$ apt-get install virtualbox
```
* Install Vagrant
Run the below command to install Vagrant
```
$ apt-get install vagrant
```
* Verify if Vagrant is installed successfully
Run the below command to check if Vagrant is installed and verify Vagrant Version
```
$ vagrant

$ vagrant -v
```
should output
```
Vagrant 2.0.2
```

## Load Ubuntu Desktop 18.04 Vagrant Box
Follow the below steps to load up Ubuntu Desktop 18.04 Vagrant Box
* Switch to Root user
```
$ sudo -s
```
* Create a project folder under which we initialize Vagrant
```
$ mkdir javadevsetup-vagrant

$ cd javadevsetup-vagrant
```
* Initialize Vagrant with one of the available Ubuntu Desktop 18.04 box available in Vagrant public boxes 
```
$ vagrant init peru/ubuntu-18.04-desktop-amd64
```
This will create file `Vagrantfile` which have reference to the used public box
* Run Vagrant command to startup using the available Vagrantfile
```
$ vagrant up
```
This will use the default provider `virtualbox` and will download the virtualbox ubuntu desktop 18.04 image and starts it up. 
You should observe something similar after running the above command
```
root@Madan:~/work/javadevsetup-vagrant# vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'peru/ubuntu-18.04-desktop-amd64' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'peru/ubuntu-18.04-desktop-amd64'
    default: URL: https://vagrantcloud.com/peru/ubuntu-18.04-desktop-amd64
==> default: Adding box 'peru/ubuntu-18.04-desktop-amd64' (v20180907.01) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/peru/boxes/ubuntu-18.04-desktop-amd64/versions/20180907.01/providers/virtualbox.box
    ==> default: Successfully added box 'peru/ubuntu-18.04-desktop-amd64' (v20180907.01) for 'virtualbox'!
==> default: Importing base box 'peru/ubuntu-18.04-desktop-amd64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'peru/ubuntu-18.04-desktop-amd64' is up to date...
==> default: Setting the name of the VM: javadevsetup-vagrant_default_1537243013315_75858
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
```
Image being dowloaded is of around ~1.36 GB and it would take couple of minutes to complete.
* Connect to Image that is loaded
```
$ vagrant ssh
```
This should output text as below and showing the bash of the guest os that is loaded
```
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-33-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


0 packages can be updated.
0 updates are security updates.

vagrant@linux:~$
```
* To access GUI instead os shell, uncomment the below piece of code in Vagrantfile to set `vb.gui` to `true` and set `vb.memory` to `3 GB`
```
config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    
    # Customize the amount of memory on the VM:
    vb.memory = "3072"
end
```
Reload the image by running the below command
```
$ vagrant reload
```
This will shutdown the running image and starts it up with the recent changes done to the Vagrantfile. Ubuntu Desktop will be loaded in the Virtualbox console with login screen displayed. Login with password `vagrant` and follow the instructions to setup ubuntu during the first time startup.

## Bootstraping Java Development Environment on Ubuntu Desktop Image
For Java Development Environment to be setup, we need to create `dev` user with which we need to login to Ubuntu Desktop.

Below are the list of SDKs, Softwares & Tools that will be configured as part of the Development Environment setup
* Java 8
* Node
* SDKMAN
* Gradle
* Maven
* SVN
* Git
* Notepad++
* Spring Tools 4
* Visual Studio Code
* Docker & Docker Compose

Follow the steps to bootstrap the environment on Ubuntu Desktop Image.

* Destroy the current machine that is managed by Vagrant
```
$ vagrant destroy
```
* Create `bootstrap.sh` file with series of commands to setup sdks, softwares & tools necessary for regular Java Development
```
#!/bin/bash

# Swicth to sudo user
sudo -s

# Create dev user
sudo useradd -m dev
sudo echo dev:dev | sudo /usr/sbin/chpasswd
sudo usermod -s /bin/bash dev
sudo adduser dev sudo

# Complete prerequisites
echo "[prerequisites] Adding repositories & performing prerequisit tasks"

## Update OS
sudo apt-get -y update && apt-get -y upgrade

## Add Repositories
sudo add-apt-repository -y ppa:webupd8team/java

## Update os
sudo apt-get -y update

## Run the below command to install necessary repositories that would be needed by some software providers
sudo apt-get install software-properties-common -y

## On Ubuntu desktop, editing any document with vi editor causes some wierd issue by printing letters on pressing arrow keys
## To disable this, run the below command. This will create the file if it does not exist
sudo echo "set nocompatible" >> $HOME/.exrc

##----------------------------------
## Install CURL
##----------------------------------
sudo apt install curl -y

##----------------------------------
## Install libconfig
##----------------------------------
sudo apt-get -y install libgconf-2-4

##----------------------------------
## Install Java8
##----------------------------------
echo "[Installing Java...]"
# automatic install of the Oracle JDK 8
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
sudo apt-get -y install oracle-java8-set-default
export JAVA_HOME="/usr/lib/jvm/java-8-oracle"

##----------------------------------
## Install SDKMAN
##----------------------------------
echo "[Installing SDKMAN...]"
sudo curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

##----------------------------------
## Install Gradle
##----------------------------------
echo "[Installing Gradle...]"
sdk install gradle 4.10.1

##----------------------------------
## Install Maven
##----------------------------------
echo "[Installing Maven...]"
sdk install maven

##----------------------------------
## Install Node
##----------------------------------
echo "[Installing Node...]"
curl o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
source ~/.bashrc
nvm install v8.12.0

##----------------------------------
## Install SVN
##----------------------------------
echo "[Installing SVN...]"
sudo apt-get -y install subversion

##----------------------------------
## Install Git
##----------------------------------
echo "[Installing Git...]"
sudo apt-get -y install git-core

##----------------------------------
## Install Notepad++
##----------------------------------
echo "[Installing Notepad++...]"
sudo snap install notepad-plus-plus

##----------------------------------
## Install Spring Tool Suite 4
##----------------------------------
echo "[Installing Spring Tool Suite 4...]"
wget http://download.springsource.com/milestone/STS4/4.0.0.M15/dist/e4.9/spring-tool-suite-4-4.0.0.M15-e4.9.0-linux.gtk.x86_64.tar.gz -O spring-tool-suite-4.tar.gz
sudo tar -xvf spring-tool-suite-4.tar.gz -C /opt
sudo ln -s /opt/sts-4.0.0.M15/SpringToolSuite4 /usr/bin/sts

##----------------------------------
## Install Visual Studio Code
##----------------------------------
echo "[Installing Visual Studio Code...]"
sudo snap install vscode --classic

##----------------------------------
## Install Postman
##----------------------------------
echo "[Installing Postman...]"
sudo snap install postman

##----------------------------------
## Install Docker & Docker Compose
##----------------------------------
echo "[Installing Docker & Docker Compose...]"
### Update
sudo apt -y update

### Add Certificates
sudo apt -y install apt-transport-https ca-certificates curl software-properties-common

### Add GPG Key for the official Docker repository
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

### Add docker repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

### Update
sudo apt -y update

### Command to use docker repo instead of ubuntu repo to install docker
sudo apt-cache policy docker-ce

### Install docker & docker compose
sudo apt -y install docker-ce
sudo apt -y install docker-compose

###Add dev user to docker group
sudo gpasswd -a dev docker
sudo service docker restart

##----------------------------------
# Configure Desktop shortcuts
##----------------------------------
## <<TODO>>
```
* Replace content in `Vagrantfile` with the content below to configure provisioner which should be executed when the image is provisioned during the first startup
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  ## Use ubuntu 18.04 desktop base
  config.vm.box = "peru/ubuntu-18.04-desktop-amd64"

  ## Virtualbox provider with GUI set to True with appropriate memory and cpu
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "3072"
  end
  
  ## Provision Bootstrap Script
  config.vm.provision :shell, path: "bootstrap.sh"
end
```
* Spinup the Image
```
$ vagrant up
```
This will load the image in VirtualBox and also execute bootstrap.sh for which we can see the logs being written in the console.

Bootstrap script execution will take time as it needs to download all the packages and have them installed. This is one time activity which will be executed during the first time startup.
