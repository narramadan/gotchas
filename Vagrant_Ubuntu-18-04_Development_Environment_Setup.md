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
