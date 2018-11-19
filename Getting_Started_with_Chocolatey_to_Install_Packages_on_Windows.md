# Getting Started with Chocolatey to Install Packages on Windows

## Install Chocolatey
Follow the steps provided [here](https://chocolatey.org/install) for complete list of requirements & options

* Search for `windows powershell` > Right Click > Choose to run as Administrator
* Run below command
```
[System.Net.WebRequest]::DefaultWebProxy.Credentials = [System.Net.CredentialCache]::DefaultCredentials; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
* If you are installing behind a Proxy, follow the below steps
  * Copy the [install.ps1](https://chocolatey.org/install.ps1) file locally.
  * Set the environment variables in the powershell console that is opened in earlier step and run the below command
  ```
  > $env:chocolateyProxyLocation = 'http://host:port'
  > $env:chocolateyProxyUser = 'username'
  > $env:chocolateyProxyPassword = 'password'
  ```
  * Install chocolatey using install.ps1 that is saved locally
  ```
  > .\install.ps1
  ```
  * If you find any issues, follow the troubleshooting tips provided [here](https://chocolatey.org/docs/proxy-settings-for-chocolatey#installing-chocolatey-behind-a-proxy-server)
* Verify if Chocolatey is installed successfully by running the below command which will be listing all of the different things you can pass to choco 
```
> choco /?
```
* To upgrade chocolatey to a newer version, run the below command
```
> choco upgrade chocolatey
```
* To uninstall chocolatey if you no longer need it, follow the steps provided [here](https://chocolatey.org/docs/uninstallation)

## Install Packages using Chocolatey

Package install/upgrade/uninstall remains the same for all the packages. Search for the appropriate package [here](https://chocolatey.org/packages) and run the commands provided below for reference to have them installed/upgraded/uninstalled.

*Note:* 
* Ensure to install packages by opening cmd/powershell with Run as Administration option
* Packages will be installed to `C:\tools` by default and will be added to `PATH`

### Install Dart SDK
Run the below command(s) to Install, Verify, Upgrade, Remove Dart SDK
```
# Install
> choco install dart-sdk

# To verify, open new cmd console
> dart 

# Upgrade
> choco upgrade dart-sdk

# Uninstall
> choco uninstall dart-sdk
```

## Chocolatey commands for reference

### Help
```
# Prints out the help menu
> choco -?

# Prints out the help menu for specific command
> choco install -?
```

### Listing packages
```
# List all versions of installed packages
> choco list -la
```

### Search packages
```
# Search for specific package
> choco search gradle
```

### Install packages
```
# Install package
> choco install gradle

# Install specific version of the package
> choco install gradle --version 3.4.1

# Installing multiple versions of the the same package, pass option -m
> choco install gradle --version 3.4.1 -my

> choco install gradle --version 4.10.2 -my
```

### Development packages
```
> choco install dart-sdk

> choco install python

> choco install nodejs.install
```
