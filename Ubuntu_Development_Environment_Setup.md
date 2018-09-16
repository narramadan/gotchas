# Java Development Setup on Ubuntu

This document is intended to setting up Java Development Environment on Ubuntu Desktop 18.04.1

We would be configuring:
* Java 8
* Node
* Gradle
* Maven
* SVN
* Git
* Spring Tool Suite
* Visual Studio Code

## Setting up Ubuntu

### Update/Upgrade Ubuntu
Run the below command in terminal to update your OS. Switch to `root` user before executing these commands
```
# apt-get update && apt-get upgrade
```
Run the below command to some necessary repositories that would be needed by some software providers 
```
# apt-get install software-properties-common
```
### Setting up vi editor
On Ubuntu desktop, editing any document with vi editor causes some wierd issue by printing letters on pressing arrow keys.

To disable this, run the below command. This will create the file if it does not exist
```
vi $HOME/.exrc
```
Add line `set nocompatible` and save the file.
### Install CURL
Run the below command to install CURL
```
apt install curl
```

## Java 8 setup
Run the below commands to install Oracle JDK 8
```
# add-apt-repository ppa:webupd8team/java

# apt-get update

# apt-get install oracle-java8-installer
```
Verify if Java is installed properly and check the version
```
# java -version
```
Output should be something like below
```
# java -version
java version "1.8.0_181"
Java(TM) SE Runtime Environment (build 1.8.0_181-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)
```
### Set a default if you have multiple Java installations
If you have multiple Java installations, you can set a default one by using the following command:
```
# update-alternatives --config java
```
You can also use this command to check if you have multiple installations.
You’ll get an output with a list of installed Javas. Press enter to keep the default one without any changes or enter a number to select a different default Java.
### Set JAVA_HOME Variable
Get Java installation path by running `update-alternatives --config java` to set JAVA_HOME environment variable.
Open `/etc/environment` and add the environment variable at the end of the file
```
# vi /etc/environment
```
Add line to the end of the file
```
JAVA_HOME="/your/java/installation-path"
```
Save the file ad then reload it
```
# source /etc/environment
```
Check if JAVA_HOME variable is set properly or not by running the below command
```
# echo $JAVA_HOME
```

## Install SDKMAN - Software Development Kit Manager
`SDKMAN` is a tool for managing parallel versions of multiple `Software Development Kits` on most unix based systems. 
It provides a convenient Command Line Interface (CLI) and API for installing, switching, removing and listing Candidates.
Run the below command to download the binaries
```
# curl -s "https://get.sdkman.io" | bash
```
Next, open a new terminal or enter:
```
# source "$HOME/.sdkman/bin/sdkman-init.sh"
```
Lastly, run the following code snippet to ensure that installation succeeded:
```
# sdk version
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
# sdkman install gradle 4.10.1 
```
To use different version of Gradle say 4.4, Install the same using above and follow the commands below to list the current version that is being used, list all versions and set one of the available as default using SDKMAN
```
# sdk current gradle

# sdk list gradle
Lists all available versions with markings for all versions, what are installed and what is being currently used

# sdk default gradle 4.4
```
If there is a new version of gradle is available and you wish to use it, run the following command to upgrade to it
```
sdk upgrade gradle
```
### Manual Installation
* Download latest version from - https://gradle.org/releases
* Unzip the distribution zip file in the directory of your choice
```
# mkdir /opt/gradle

# unzip -d /opt/gradle gradle-4.10.1-bin.zip

# ls /opt/gradle/gradle-4.10.1
```
* Configure PATH environment variable to include the `bin` directory
```
# export PATH=$PATH:/opt/gradle/gradle-4.10.1/bin
```
* Verify if gradle is configured correctly
```
# gradle -v
```

## Setup Maven
```
sdk install maven
```

## Setup Spring Boot
Spring Boot CLI is a command line tool that can be used to quickly prototype with Spring. This will provide a quickest wat to get a Spring application kickstarted
```
sdk install springboot
```

## Setup Node
Node can be installed using `nvm` Node Version Manager or manually.

### Installation via NVM
Follow the series of command to install node via nvm
* Run `nvm` installer
```
# curl o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

The script clones the nvm repository to ~/.nvm and adds the source line to your profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc)
```
* Reload the shell
```
# source ~/.bashrc
```
* Verify if nvm is installed correctly
```
# command -v nvm
```
* List all versions of node that are installed
```
# nvm ls
```
* If none available, install specific version of nodejs
```
# nvm install v8.12.0
```
* Verify if Nodejs & NPM are installed correctly
```
# node -v

# npm -v
```
* To use a different version of node during development
```
# npm use 8.6.0
```
* To uninstall a specific version if it is no longer needed
```
# nvm uninstall 8.6.0
```

### Manual Installation
* Download the package and install it
```
# curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

# sudo apt-get install -y nodejs
```
* Verify if nodejs is installed correctly
```
# node -v
```
* Check where node is installed
```
# which node
```

## Install SVN
```
# apt-get install subversion

# svn --version
```

## Install Git
```
# apt-get install git-core

# git --version
```
### Configure and view git settings
```
# git config --global user.name "<YOUR NAME>"
# git config --global user.email "<YOUR EMAIL>"

# cat ~/.gitconfig

# git config --list
```

## Install IntelliJ IDEA

## Install Spring Tool Suite

## Install Visual Studio Code