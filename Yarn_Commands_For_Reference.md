# Yarn commands for reference

## Install or Upgrade
`npm install -g yarn` - To either install yarn globally or upgrade to the later version

## Handling Global Packages

`yarn global` is the prefix to handle global packages

`yarn global add <package>` - Install

`yarn global list` - List all global packages installed

`yarn global upgrade <package>` - Update the package

`yarn global remove <pakage>` - Uninstall

`yarn global bin` - Location where the global packages are installed and set in system path

## Handling Local Packages

`yarn install` - Install dependencies listed in package.json

`yarn add <package>` - Install

`yarn upgrade --latest` - Upgrade all dependencies to their latest versions. This will only upgrade dependencies but not package.json

`yarn upgrade-interactive --latest` - Upgrades all dependencies to their latest versions by confirming with the user for each dependency. This will onlu upgrade dependencies but not package.json

`yarn upgrage <package> <package@version>` - Upgrade one or more packages with or without version

`yarn remove <package>` - Uninstall package

`yarn list` - List all packages with their versions installed locally with their `dependencies` as well

`yarn list --depth=0|1|2` - List all packages with the specified depth of dependencies

`yarn list --pattern <package|package>` - list packages with the specified pattern

## Quick References

`yarn add <git remote url>#<branch/commit/tag>` - installs a package from a remote git repository at specific git branch, git commit or git tag

`yarn create <starter-kit-package>` - Creates new projects from any `create-*` starter kits. This is alternative to adding the package globally and invoking the package command.
```
yarn global add create-react-app
create-react-app my-app
```
## Fixing Common Issues

### Fix `Error: watch ENOSPC` on Ubuntu when running `yarn dev`
I had this problem when running `yarn dev` or `npm start` no a Ubuntu 18.04

This [link](https://discourse.roots.io/t/gulp-watch-error-on-ubuntu-14-04-solved/3453) helped me on this, The error happens because there's a limit of files that can be watched by default on Ubuntu. And we need to increase this number of files in the `/etc/sysctl.conf` config file, adding this line at the end `fs.inotify.max_user_watches=582222`

The command to add the config bellow is

`echo fs.inotify.max_user_watches=582222 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

### Fix `libpng12.so.0: cannot open shared object file: No such file or directory` on Ubuntu
Run the below command to fix issue on not finding `libpng12.so`
```
echo "deb http://mirrors.kernel.org/ubuntu/ xenial main" | sudo tee -a /etc/apt/sources.list && sudo apt-get update && sudo apt install -y --allow-unauthenticated libpng12-0
```
