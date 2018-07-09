# Yarn commands for reference

## Handling Global Packages

`yarn global` is the prefix to handle global packages

`yarn global add <package>` - Install

`yarn global list` - List all global packages installed

`yarn global upgrade <package>` - Update the package

`yarn global remove <pakage>` - Uninstall

`yarn global bin` - Location where the global packages are installed and set in system path

## Handling Local Packages

`yarn add <package>` - Install

`yarn upgrage <package> <package@version>` - Upgrade one or more packages with or without version

`yarn remove <package>` - Uninstall package

`yarn list` - List all packages with their versions installed locally with their `dependencies` as well

`yarn list --depth=0|1|2` - List all packages with the specified depth of dependencies

`yarn list --pattern <package|package>` - list packages with the specified pattern
