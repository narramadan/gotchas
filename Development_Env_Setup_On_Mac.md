# Development Environment setup on Macbook

[Mac Cheat Sheets](https://www.makeuseof.com/tag/mac-terminal-commands-cheat-sheet/)

## Browsers
* Microsoft Edge
* Google chrome

## Collobration
* Microsoft Teams

## Utilities
### Flycut - Clipboard manager

- Can be installed from appstrore.

### Boop - Developer Tool

- Can be installed from appstrore.

### [Tabby terminal](https://tabby.sh/)

Install latest macos package(tabby-1.0.197-macos-arm64.pkg)

To display git branch names and other stylings, install [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)

Run the below command post installing Tabby terminal, for the terminal to instantly change with default theme.

```
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Post installing `zsh`, need to do the below to load bash alises into zsh.

```
$ vi ~/.zshrc

Copy below at the bottom of the file

source ~/.bash_profile

:wq

$ source ~/.zshrc
```

### Sublime Text

- Use this as replaced for Notepad++ on Windows

### Json Viewer

Native Mac app to visualize, validate and format JSON datasets - https://jsonviewer.app/

## Applications

### IntelliJ IDEA

Download and install IntelliJ IDEA Community Edition.

Install below plugins after launching.

* Cucumber for Java
* Markdown

### VSCode

Download VSCode archive and extract the content. Move the extracted app file to applications.

Install below extensions by launching `VS Code Quick Open (⌘+P)`

```
ext install zesbenp.prettier-vscode

ext install donjayamanne.githistory

ext install johnpapa.vscode-peacock

ext install vscjava.vscode-java-pack

ext install redhat.java

ext install vscjava.vscode-java-debug

ext install vscjava.vscode-java-dependency

ext install vscjava.vscode-maven

ext install vscjava.vscode-java-test

ext install eamodio.gitlens

ext install VisualStudioExptTeam.vscodeintellicode

ext install ms-vscode-remote.remote-containers

ext install ms-azuretools.vscode-docker

ext install ms-kubernetes-tools.vscode-kubernetes-tools
```

### Docker Desktop

Post installation, navigate to settings and enable kubernetes cluster.

Run the below commands to verify if installation and configuration is successful.

```
$ docker -v

$ kubectl version
```

### Postman

Download Postman archive and extract the content. Move the extracted app file to applications.

## Binaries

### Homebrew

Execute the below in terminal
```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Run the below to add homebrew to path
```
$ (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/madan/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
```

Run the below to verify if brew is installed successfully and available in the path for subsequent commands

```
$ brew search java
```

### Curl

```
$ brew install curl

$ curl --help
```

### SDKMAN

```
$ curl -s "https://get.sdkman.io" | bash

$ source "$HOME/.sdkman/bin/sdkman-init.sh"

$ sdk version

$ sdk list
```

### Java

#### Elcipse Temurin Distro 

Install latest version of OpenJDK distribution from [Eclipse Temurin](https://adoptium.net/temurin/releases/).

https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.7%2B7/OpenJDK17U-jdk_aarch64_mac_hotspot_17.0.7_7.pkg

```
$ java --version
```

To uninstall, run the below command

`$ rm -rf /Library/Java/JavaVirtualMachines/temurin-17.jdk`

#### Using SDKMAN

Identify and choose the version of Java that you wish to install 

```
$ sdk list java

$ sdk install java 8.0.372-zulu

$ java -version
```

Install another version of Java. Post installation, prompt would appear to choose this version as default. Opt in accordingly.

```
$ sdk install java 11.0.19-zulu
```

To switch between versions of Java, use the below commands

```
# See which versions are installed
$ sdk list java 

$ sdk use java 11.0.19-zulu
```

To set a permanent default, use the sdk default command. For instance, to make JDK 11 the default, type:

```
$ sdk default java 11.0.0-open
```


### Maven

```
$ brew install maven

$ mvn -v
```

### Gradle

```
$ brew install gradle

$ mvn -v
```

### Git

```
$ brew install git

$ git -v
```

### mitmweb

[mitmproxy](https://mitmproxy.org/) is a free and open source interactive HTTPS proxy. 

```
$ brew install mitmproxy
```

### Node

```
$ brew install node

$ node -v

$ npm -v

$ npm install -g yarn

$ yarn -v
```

### Mockoon

[Mockoon](https://mockoon.com/) is the easiest and quickest way to design and run mock REST APIs

```
brew install --cask mockoon
```

## MacOS Customizations

### Choose Open with VSCode for selected folder from finder

https://stackoverflow.com/questions/64040393/open-a-folder-in-vscode-through-finder-in-macos
