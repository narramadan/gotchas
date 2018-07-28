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
