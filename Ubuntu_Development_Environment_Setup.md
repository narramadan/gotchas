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
