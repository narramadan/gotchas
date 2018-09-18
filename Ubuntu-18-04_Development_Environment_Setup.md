# Java Development Environment Setup on Ubuntu 18.04

This document is intended to setting up Java Development Environment on Ubuntu Desktop 18.04.1

We would be configuring:
### Runtimes 
* Java 8
* Node

### Development Tools
* Gradle
* Maven
* SVN
* Git

### IDEs
* Notepad++
* IntelliJ IDEA
* Spring Tool Suite
* Visual Studio Code

### Additional Softwares or Packages
* Docker
* MariaDB
* MongoDB

### Testing Tools
* Postman

## Setting up Ubuntu

### Update/Upgrade Ubuntu
Run the below command in terminal to update your OS. Switch to `root` user before executing these commands
```
$ apt-get update && apt-get upgrade
```
Run the below command to some necessary repositories that would be needed by some software providers 
```
$ apt-get install software-properties-common
```

### Setting up vi editor
On Ubuntu desktop, editing any document with vi editor causes some wierd issue by printing letters on pressing arrow keys.

To disable this, run the below command. This will create the file if it does not exist
```
$ vi $HOME/.exrc
```
Add line `set nocompatible` and save the file.

### Install CURL
Run the below command to install CURL
```
$ apt install curl
```

### Install libconfig
Libconfig is removed from Ubuntu 18 and this has to be installed to get Postman working. Run the below command to install it
```
$ sudo apt-get install libgconf-2-4
```

## Java 8 setup
Run the below commands to install Oracle JDK 8
```
$ add-apt-repository ppa:webupd8team/java

$ apt-get update

$ apt-get install oracle-java8-installer
```
Verify if Java is installed properly and check the version
```
$ java -version
```
Output should be something like below
```
$ java -version
java version "1.8.0_181"
Java(TM) SE Runtime Environment (build 1.8.0_181-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)
```
### Set a default if you have multiple Java installations
If you have multiple Java installations, you can set a default one by using the following command:
```
$ update-alternatives --config java
```
You can also use this command to check if you have multiple installations.
You’ll get an output with a list of installed Javas. Press enter to keep the default one without any changes or enter a number to select a different default Java.
### Set JAVA_HOME Variable
Get Java installation path by running `update-alternatives --config java` to set JAVA_HOME environment variable.
Open `/etc/environment` and add the environment variable at the end of the file
```
$ vi /etc/environment
```
Add line to the end of the file
```
JAVA_HOME="/your/java/installation-path"
```
Save the file ad then reload it
```
$ source /etc/environment
```
Check if JAVA_HOME variable is set properly or not by running the below command
```
$ echo $JAVA_HOME
```

## Install SDKMAN - Software Development Kit Manager
`SDKMAN` is a tool for managing parallel versions of multiple `Software Development Kits` on most unix based systems. 
It provides a convenient Command Line Interface (CLI) and API for installing, switching, removing and listing Candidates.
Run the below command to download the binaries
```
$ curl -s "https://get.sdkman.io" | bash
```
Next, open a new terminal or enter:
```
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```
Lastly, run the following code snippet to ensure that installation succeeded:
```
$ sdk version
```
If all went well, the version should be displayed. Something like:
```
SDKMAN 5.7.2+323
```
## Setup Gradle
Gradle can be installed and configured either via SDKMAN or manually. It is always preferrable to use SDKMAN as it eases the developer time and effort to switch to the appropriate version when different projects use different versions of gradle
### Installation via SDKMAN
Run the below command to install Gradle using SDKMAN Package Manager
```
$ sdk install gradle 4.10.1 
```
To use different version of Gradle say 4.4, Install the same using above and follow the commands below to list the current version that is being used, list all versions and set one of the available as default using SDKMAN
```
$ sdk current gradle

# sdk list gradle
Lists all available versions with markings for all versions, what are installed and what is being currently used

$ sdk default gradle 4.4
```
If there is a new version of gradle is available and you wish to use it, run the following command to upgrade to it
```
sdk upgrade gradle
```
### Manual Installation
* Download latest version from - https://gradle.org/releases
* Unzip the distribution zip file in the directory of your choice
```
$ mkdir /opt/gradle

$ unzip -d /opt/gradle gradle-4.10.1-bin.zip

$ ls /opt/gradle/gradle-4.10.1
```
* Configure PATH environment variable to include the `bin` directory
```
$ export PATH=$PATH:/opt/gradle/gradle-4.10.1/bin
```
* Verify if gradle is configured correctly
```
$ gradle -v
```

## Setup Maven
```
$ sdk install maven
```

## Setup Spring Boot
Spring Boot CLI is a command line tool that can be used to quickly prototype with Spring. This will provide a quickest wat to get a Spring application kickstarted
```
$ sdk install springboot
```

## Setup Node
Node can be installed using `nvm` Node Version Manager or manually.

### Installation via NVM
Follow the series of command to install node via nvm
* Run `nvm` installer
```
$ curl o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

The script clones the nvm repository to ~/.nvm and adds the source line to your profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc)
```
* Reload the shell
```
$ source ~/.bashrc
```
* Verify if nvm is installed correctly
```
$ command -v nvm
```
* List all versions of node that are installed
```
$ nvm ls
```
* If none available, install specific version of nodejs
```
$ nvm install v8.12.0
```
* Verify if Nodejs & NPM are installed correctly
```
$ node -v

$ npm -v
```
* To use a different version of node during development
```
$ npm use 8.6.0
```
* To uninstall a specific version if it is no longer needed
```
$ nvm uninstall 8.6.0
```

### Manual Installation
* Download the package and install it
```
$ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

$ sudo apt-get install -y nodejs
```
* Verify if nodejs is installed correctly
```
$ node -v
```
* Check where node is installed
```
$ which node
```

## Install SVN
```
$ apt-get install subversion

$ svn --version
```

## Install Git
```
$ apt-get install git-core

$ git --version
```
### Configure and view git settings
```
$ git config --global user.name "<YOUR NAME>"
$ git config --global user.email "<YOUR EMAIL>"

$ cat ~/.gitconfig

$ git config --list
```

## Install Notepad++
Run the below command to install IntelliJ IDEA Community edition
```
$  sudo snap install notepad-plus-plus
```

## Install IntelliJ IDEA
Run the below command to install IntelliJ IDEA Community edition
```
$  sudo snap install intellij-idea-community --classic --edge
```

If this fails, try to search for `intellij-idea-community` and choose to install the app from Ubuntu Software app.

## Install Spring Tool 4
Follow the below steps to Install Spring Tool Suite
* Download Spring Tools 4
```
$ wget http://download.springsource.com/milestone/STS4/4.0.0.M15/dist/e4.9/spring-tool-suite-4-4.0.0.M15-e4.9.0-linux.gtk.x86_64.tar.gz -O spring-tool-suite-4.tar.gz
```
* Extract the downloaded file to /opt
```
$ sudo tar -xvf spring-tool-suite-4.tar.gz -C /opt
```
* Create Symbolic link
```
$ sudo ln -s /opt/sts-4.0.0.M15/SpringToolSuite4 /usr/bin/sts
```
* Create Desktop Entry
```
$ cat > ~/.local/share/applications/sts.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=STS
Exec=sts
Icon=//opt/sts-4.0.0.M15/icon.xpm
Terminal=false
Type=Application
Categories=Development;
EOL
```
* Launch STS by typing `sts` anywhere in terminal or search under installed apps

## Install Visual Studio Code
Run the below command to install Visual Studio Code
```
$ sudo snap install vscode --classic
```

## Install Postman
Run the below command to install Postman Native app
```
$ sudo snap install postman
```

## Install Docker
Docker should be installed from the official Docker repository rather then from the official Ubuntu repository as the Docker Installation package might not be the latest version.

Follow the series of commands to install Docker on Ubuntu
* Update packages & few prerequisite packages
```
$ apt update

$ apt install apt-transport-https ca-certificates curl software-properties-common
```
* Add GPG key for the official Docker repository
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
* Add the Docker repository to APT sources
```
$ add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```
* Update the package database with the Docker packages from the newly added repo
```
$ apt update
```
* Run the below command which will use the Docker repo instead of Ubuntu repo for the installation
```
$ apt-cache policy docker-ce
```
* Running the below command will install Docker and start the service as daemon and have the process enabled to start during system boot
```
$ apt install docker-ce
```
* Verify if Docker is started and running
```
$ systemctl status docker
```
Output should be something like below
```
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: e
   Active: active (running) since Mon 2018-09-17 11:44:56 AEST; 2min 10s ago
     Docs: https://docs.docker.com
 Main PID: 5165 (dockerd)
    Tasks: 38
   CGroup: /system.slice/docker.service
           ├─5165 /usr/bin/dockerd -H fd://
           └─5193 docker-containerd --config /var/run/docker/containerd/containe
```
### Configure Docker command to run without Sudo
Follow the below commands to configure to run Docker commands without Sudo
* Add `username` to the `docker` group. Before running this, make sure you exit for root user
```
$ sudo usermod -aG docker ${USER}
```
* Close the current terminal and start new one and run the below command to apply the new group membership
```
$ su - ${USER}
```
* Verify if the user is added to the `docker` group
```
$ id -nG
```
It should output something like this
```
madan adm cdrom sudo dip plugdev lpadmin sambashare docker
```
* Verify running the docker command without sudo and check if you can see the subcommands listed
```
$ docker
```

## Install MariaDB
Follow the below series of steps to install & configure MariaDB on Ubuntu 18.04
* Add MariaDB repository
```
$ sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8

$ sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] http://ftp.utexas.edu/mariadb/repo/10.3/ubuntu bionic main'

$ sudo apt update
```
* Install MariaDB
```
$ sudo apt install mariadb-server
```
* Verify if MariaDB is installed and up & running
```
$ sudo systemctl status mariadb
```
Output should be something like below
```
● mariadb.service - MariaDB 10.3.9 database server
   Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: 
  Drop-In: /etc/systemd/system/mariadb.service.d
           └─migrated-from-my.cnf-settings.conf
   Active: active (running) since Mon 2018-09-17 18:31:36 AEST; 15s ago
     Docs: man:mysqld(8)
           https://mariadb.com/kb/en/library/systemd/
 Main PID: 18985 (mysqld)
   Status: "Taking your SQL requests now..."
    Tasks: 32 (limit: 4915)
   CGroup: /system.slice/mariadb.service
           └─18985 /usr/sbin/mysqld

```
* Login to MariaDB with the `root` user and password provided during installation
```
$ mysql -u root -p
```
* Stop & Start MariaDB Service
```
-- Stop the service
$ sudo systemctl stop mariadb.service

-- Start the service
$ sudo systemctl start mariadb.service

-- Enable the service to be started during bootup
$ sudo systemctl enable mariadb.service

-- Restart the service
$ sudo systemctl restart mariadb.service
```

## Install MongoDB
Follow the below series of steps to install & configure MongoDB on Ubuntu 18.04
* Add MongoDB repository
```
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4

$ echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list

$ sudo apt-get update
```
* Install MongoDB
```
$ sudo apt-get install -y mongodb-org
```
* Install specific version of MongoDB
```
$ sudo apt-get install -y mongodb-org=4.0.2 mongodb-org-server=4.0.2 mongodb-org-shell=4.0.2 mongodb-org-mongos=4.0.2 mongodb-org-tools=4.0.2
```
* Start the service and verify if it is up & running
```
$ sudo service mongod start

$ sudo systemctl status mongod
```
Output should be something like below
```
● mongod.service - MongoDB Database Server
   Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: 
   Active: active (running) since Mon 2018-09-17 18:49:09 AEST; 4s ago
     Docs: https://docs.mongodb.org/manual
 Main PID: 21387 (mongod)
   CGroup: /system.slice/mongod.service
           └─21387 /usr/bin/mongod --config /etc/mongod.conf

Sep 17 18:49:09 Madan systemd[1]: Started MongoDB Database Server.

```
* Connect to MongoDB
```
$ mongo --host 127.0.0.1:27017
```
* Stop & Start MariaDB Service
```
$ sudo service mongod stop

$ sudo service mongod start

$ sudo service mongod restart
```
