# Git Commands for Reference

* https://git-scm.com/docs
* https://services.github.com/on-demand/github-cli/
* https://makandracards.com/makandra?query=topic%3A%22Version+control%22

## Setup

For [Windows](https://git-scm.com/download/win)

Which version of Git for Windows are you using? Is it 32-bit or 64-bit?
```
$ git --version --build-options
```

## Configuration
`git config --global user.name "<name of the user>"` - Configure global User Name

`git config --global user.email "<email>"` - Configure global email address

`git config --list` - list all git configurations

Configurations are stored in `C:\ProgramData\Git\config` on Windows and `/etc/gitconfig` on unix platforms in `.gitconfig` file.

## Working with Git behind http proxy
`git config --global http.proxy http://proxyuser:proxypwd@proxy.server.com:proxy.server.port` - Command to configure http proxy

* change `proxyuser` to your proxy user
* change `proxypwd` to your proxy password
* change `proxy.server.com` to the URL of your proxy server
* change `proxy.server.port` to the proxy port configured on your proxy server

`git config --global --get http.proxy` - to verify if proxy is set correctly.

`git config --global --unset http.proxy` - to remove the proxy configuration 

## Create
`git clone <url>` - Clone a repository

`git clone -b <branch> --single-branch <url>` - Clone a specific branch of a repository

`git clone <url> <foldername>` - Clone a repository to the provided folder name

`git init` - Initialize new local git repository in an existing folder

## Working with Changes
`git add -u` - Consider files or folders deleted to be committed with `commit` and pushed with `push` commands

## See Commit History

## Update the local repository

## Push changes to remote repository

## Working with Branches & Tags

### Fetch
`git fetch` - fetch branches and/or tags from one or more repositories

`git fetch origin` - It copies all branches from the remote references and store them to the local references

`git fetch -p` - Before fetching, it will remove any remote-tracking references that no longer exists on the remote.

### List
`git branch` - Lists down all branches available locally with * mapped to the current working branch

`git branch -r` - Lists all remote branches 

`git branch -a` - List all remote and local branches

### Manage

#### Create new Local Branch
`git branch <local_branch_name>` - Create a new local branch

`git checkout <branch_name>` - Switch to the selected branch

#### Check out a remote branch
`git fetch origin` - It copies all branches from the remote references and store them to the local references

`git checkout <branch_name>` - Switch to the selected branch

### Delete
`git branch -d <branch_name>` - Delete a local branch

`git push origin --delete <branch_name>` - Delete a remote branch

## Merging & Rebasing

## Revert changes

## Stashing your work

## Git Inteview Questions

### Git Cherry Pick vs Rebase