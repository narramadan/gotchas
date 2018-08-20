# Git Commands for Reference

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

## Create
`git clone <url>` - Clone a repository

`git clone -b <branch> --single-branch <url>` - Clone a specific branch of a repository

`git clone <url> <foldername>` - Clone a repository to the provided folder name

`git init` - Initialize new local git repository in an existing folder

## Working with Changes

## See Commit History

## Update the local repository

## Push changes to remote repository

## Working with Branches & Tags

## Merging & Rebasing

## Revert changes

## Stashing your work

## Git Inteview Questions

### Git Cherry Pick vs Rebase
