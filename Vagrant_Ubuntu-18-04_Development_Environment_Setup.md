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
* To access GUI instead os shell, uncomment the below piece of code in Vagrantfile to set `vb.guie` to `true` and set `vb.memory` to `3 GB`
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
