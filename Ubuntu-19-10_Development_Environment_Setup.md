# Settingup Developer environment on Ubuntu 19.10

## Install curl

```
sudo apt install curl
```

## Install wger

```
sudo apt-get install wget
```

## Install libz - needed for building graalvm native image

```
sudo apt-get update -y
sudo apt-get install -y libz-dev
```

## Install sdkman

* open a new terminal and enter:

```
$ curl -s "https://get.sdkman.io" | bash
```

* Open new terminal and exter below command

```
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

* Verify if installed properly by checking version

```
$ sdk version
```

## Install GraalVM

* Download GraalVM JDK8

```
$ cd /home/<user>/Downloads

$ wget https://github.com/graalvm/graalvm-ce-builds/releases/download/vm-20.0.0/graalvm-ce-java8-linux-amd64-20.0.0.tar.gz

$ tar -xvzf graalvm-ce-java8-linux-amd64-20.0.0.tar.gz
```

* Move the unpacked dir to /usr/lib/jvm/ and create a symbolic link to make your life easier when updating the GraalVM version:

```
$ sudo mv graalvm-ce-java8-20.0.0/ /usr/lib/jvm/
```

* Install the the Graalvm Java

```
$ sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/bin/java 1
```

* verify by checking the version number:

```
$ java -version
```

* Set Path by adding below exports to anywhere above end of the file. Restart the terminal.

```
$ vi ~/.bashrc

export JAVA_HOME=/usr/lib/jvm/
export PATH=${PATH}:${JAVA_HOME}/bin
```

* Download Native image installer component package

```
$ cd /home/<user>/Downloads

$ wget https://github.com/graalvm/graalvm-ce-builds/releases/download/vm-20.0.0/native-image-installable-svm-java8-linux-amd64-20.0.0.jar
```

* Install Native Image using GraalVM Updater

```
$ gu -L install native-image-installable-svm-java8-linux-amd64-20.0.0.jar
```

* Verify if native-image is installed 

```
$ gu list
```

* Test native image

```
$ mkdir /home/<user>/learning/java

$ vi HelloWorld.java
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}

$ javac HelloWorld.java

$ native-image HelloWorld

$ ./helloworld
```

## Install maven

```
$ sdk install maven

$ mvn -v
```

## Install Gradle

```
$ sdk install gradle
$ gradle -v
```

## Install Kotlin

```
$ sdk install kotlin
$ kotlin -version
```

## Install Git

```
$ sudo apt install git
$ git --version
```

## Install Nodejs

```
$ curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
$ sudo apt-get install -y nodejs
$ sudo apt-get install -y npm
```
* Verify version

```
$ node --version
$ npm --version
```

## Install Docker

```
$ sudo apt-get update
$ sudo apt install docker.io
```

* Start and Automate Docker

```
$ sudo systemctl start docker
$ sudo systemctl enable docker
```

* Verify Version

```
$ docker --version
```

## Install microk8s

```
$ sudo snap install microk8s --classic
```

* Join user group

```
$ sudo usermod -a -G microk8s $USER
$ su - $USER
```

* verify installation

```
$ microk8s.kubectl get nodes
```

* Create alias for kubectl

```
$ vi ~/.bashrc
$ alias k='microk8s.kubectl'
```

* configure firewall to allow pod-to-pod and pod-to-internet communication:

```
$ sudo ufw allow in on cni0 && sudo ufw allow out on cni0
$ sudo ufw default allow routed
```

## Install softwares from Ubuntu Software
* chromium
* koncole terminal
* Notepadqq
* Visual Studio Code
* IntelliJ IDEA Community

## Install MariaDB

## Install Mongo DB

## Install Postman
