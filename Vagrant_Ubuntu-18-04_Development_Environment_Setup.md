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
```
Image being dowloaded is of around ~1.36 GB and it would take couple of minutes to complete.
