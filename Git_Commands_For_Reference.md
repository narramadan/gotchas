# Git Commands for Reference

* https://git-scm.com/docs
* https://services.github.com/on-demand/github-cli/
* https://makandracards.com/makandra?query=topic%3A%22Version+control%22

## Bitbucket Setup
* [Setup SSH Keys](https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html)
* [Changing remote url from https to ssh](https://help.github.com/articles/changing-a-remote-s-url/)

## Setup

For [Windows](https://git-scm.com/download/win)

Which version of Git for Windows are you using? Is it 32-bit or 64-bit?
```
$ git --version --build-options
```

If Committing files with name more then 260 characters limit on windows, It throws `Filename too long` error when running `git add *`. To overcome this, run the following command
`
git config --system core.longpaths true
`

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

## Git GUI
`gitk` - Opens Git GUI on the current branch

`gitk --all` - Opens Git GUI with all branches

## Create
`git clone <url>` - Clone a repository

`git clone -b <branch> --single-branch <url>` - Clone a specific branch of a repository

`git clone <url> <foldername>` - Clone a repository to the provided folder name

`git init` - Initialize new local git repository in an existing folder

## Working with Changes
`git add -u` - Consider files or folders deleted to be committed with `commit` and pushed with `push` commands

## See Commit History
`git log --oneline` - To see all commits one line per commit

`git log --branches --not --remotes` - To see all commits on all branches that aren't pushed yet

`git log --branches --not --remotes --simplify-by-decoration --decorate --oneline` - To see the most recent commit on each branch, and the branch names

`git reflog` - Reference logs, or "reflogs", record when the tips of branches and other references were updated in the local repository

## Update the local repository

## Push changes to remote repository

## Working with Branches & Tags

`git branch -v` - Will show, for each local branch, whether it's "ahead" or not.

`git tag` - Lists all tags

`git tag --list` - 

### Fetch
`git fetch` - fetch branches and/or tags from one or more repositories

`git fetch origin` - It copies all branches from the remote references and store them to the local references

`git fetch -p` - Before fetching, it will remove any remote-tracking references that no longer exists on the remote.

### List
`git branch` - Lists down all branches available locally with * mapped to the current working branch

`git branch -r` - Lists all remote branches 

`git branch -a` - List all remote and local branches

### Manage

### Describe

`git describe --exact-match --tags` - Display current checkout tag in local

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

### Clean
`git clean -n` - Lists untracked files which will be cleaned

`git clean -f` - Will delete untracked files

`git clean -f -d` or `git clean -fd` - Will delete untracked directories and files

`git clean -d -x -f` - Will remove untracked files (-f), including directories (-d) and files ignored by git (-x).

`git clean -d -x -i` - Will start the interactive mode (-i) of the untracked files, including directories (-d) and files ignored by git (-x)

### Reset
`git reset` - Unstage all changes

`git reset <file>` - Unstage a specific file

`git reset --hard` - To reset the entire repository to the last committed state in local branch 

`git reset --hard origin/<remote-branch>` - To reset the entire repository to the last committed state from remote branch

## Stashing your work

## Revert to previous pushed commit

Follow the below commands in sequence to revert current working branch to previously pushed commit

```
$ git reset --hard COMMIT_ID
$ git reset HEAD~1
$ git stash
$ git add .
$ git commit -m "your new commit message here"
$ git push --force
```

## miscellaneous
### Add Remote Git Repository to the local repository
Below are the series of steps to achieve this
* `git remote add origin <REPO_URL>` - Add remote git repo to the local repository
* `git remote -v` - Verify if the remote git repo is added. This should display the below messages in the console
```
> origin <REPO_URL> (fetch)
> origin <REPO_URL> (push)
```
* `git push --set-upstream origin <BRANCH>` - Set the default upstream origin branch and push the changes to repo

### Changing Remote Git Repository url to the local repository
Below are the series of steps to point the local repo to new remote repo
* `git remote -v` - Verify the current remote repo it is pointing to
* `git remote set-url origin <NEW_REPO_URL>` - run the command with new repo url
* `git remote -v` - Verify if the remote repo is pointing to the new repo

### Rempove File/Folder from git repository without deleting it from local filesystem
Below are the series of steps to achieve this
* Add entries of the file or folder in `.gitignore` so the will be excluded from the repsotory 
* `git rm -r --cached File-or-FolderName` - Delete the entries of the file or folder from git cache
* `git commit -m "Removed folder from repository"` - Commit the Changes
* `git push` - Push the changes

## Git Inteview Questions

### Git Cherry Pick vs Rebase
