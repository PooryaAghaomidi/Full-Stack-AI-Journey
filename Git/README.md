# Git tutorial

<p align="center">
  <img src="Images/git.jpg" width="400"/>
</p>

## Table of Contents

- [Installation](#installation)
- [Introduction](#introduction)
- [Section One: Git](#section-one-git)
- [Section Two: GitHub](#section-two-github)
- [Section Three: undo](#section-three-undo)
- [Section Four: Advanced](#section-four-advanced)

## Installation

Download and install git from the official website: https://git-scm.com

Then you can run git commands on your command shell (e.g. git bash, CMD, PowerShell, etc.)

## Introduction

Git is a distributed version control system that tracks versions of files. It is often used to control source code by
programmers collaboratively developing software.

## Section One: Git

### Intro

* `git --version`: get version
* `git config --global user.name "<your username>"`: set username (use global to set the username and e-mail for every
  repository)
* `git config --global user.email "<your email>"`: set email
* `git config --list`: list configuration

### General

* `git init`: initialize a git repository in the current folder (git creates a hidden folder to keep track of changes)
* `git add <your file>`: add that file to the staging environment (staged files are files that are ready to be committed
  to the repository)
* `git add -A`: add all files to the staging environment
* `git commit -m "<your message>"`: move from stage to commit (adding commits keep track of our progress and changes as
  we work)
* `git commit -m .`: commit without a message

### Info

* `git status`: display information about the status of that repository
* `git status --short`: display information in a more compact way
* `git log`: view the history of commits for a repository
* `git <command> -help`: help remembering the specific option for a command
* `git help --all`: list all possible commands

### Branch

* `git branch <branch name>`: create a new branch (a branch is a separate version of the main repository)
* `git branch -a`: list all branches and master in local and remote repositories (master/main is the primary branch of a
  repository)
* `git branch -d <branch name>`: delete the branch
* `git checkout <branch name>`: moving from the current branch to the one specified (changes the local drive so that it
  reflects the destination branch)
* `git merge <branch name>`: merge master with the branch (solve conflicts if necessary)

### Tag

* `git tag`: list all tags (versions) in the repository
* `git tag -a <your version> -m "<your message>`: assign a version to the current HEAD with an optional message (HEAD is
  the current commit)
* `git push origin <your version>`: push a version to the remote repository
* `git tag -d <your version>`: delete a version
* `git checkout <your version>`: moving from the current branch to the version
* `git tag <your version> <commit hash>`: assign a version to a specific commit

## Section Two: GitHub

### Concepts

`GitHub`: GitHub is a developer platform that allows developers to create, store, manage and share their code. It uses
Git software, providing the distributed version control of Git plus access control, bug tracking, software feature
requests, task management, continuous integration, and wikis for every project

`Note`: In GitHub you can submit a pull request to compare and merge your branches into the main branch (no code
required)

`Work flow`: The GitHub flow works like this:

1. Create a new Branch
2. Make changes and add Commits
3. Open a Pull Request
4. Review
5. Deploy
6. Merge

`Fork`: a fork is a copy of a repository. This is useful when you want to contribute to someone else's project or start
your own project based on theirs. fork is not a command in Git, but something offered in GitHub and other repository
hosts

`Note`: if the cloned repository is not ours, we are not allowed to make changes and we'd better to rename it from
origin to upstream

`Note`: after changing the repository, we can push the changes to our fork and then submit a pull request to the main
remote repository in GitHub (no code required)

### Codes

* `git remote add origin <GitHub URL>`: connect the local repository to the remote one on GitHub (origin refers to the
  remote repository)
* `git push origin main`: transfer the main branch of the local repository to the remote one on GitHub (origin/main
  refers to the main branch of the remote repository)
* `git fetch origin`: get the updates of the remote repository
* `git diff <branch name>`: display changes of a branch considering the current branch (we assume that origin/main is a
  branch)
* `git pull origin`: fetch + merge (get all changes and commits from the remote repository)

<p align="center">
  <img src="Images/overview.png" width="600"/>
</p>

* `git clone <repository URL>`: transfer a remote repository to your current folder
* `git remote rename origin upstream`: rename the remote repository from origin to upstream
* `git remote add origin <fork repository URL>`: fetch our fork of this repository to the same local one
* `git remote -v`: display all remote versions of this repository

## Section Three: Undo

* `git revert HEAD~<the number of earlier commit>`: take a previous commit and add it as a new commit, keeping the log
  intact
* `git reset <commit hash>`: move the repository back to a previous commit
* `git commit --amend <change>`: modify the most recent commit

## Section Four: Advanced

### Concepts

`.gitignore`: git can specify which files or parts of your project should be ignored by Git using a .gitignore file. git
will not track files and folders specified in .gitignore, however, the .gitignore file itself IS tracked by Git.

`Note`: it is possible to have additional .gitignore files in subdirectories that only apply to files or folders within
that directory.

`Note`: general rules for matching patterns in .gitignore files:

  1. Lines starting with `#` are ignored
  2. name -> All name files, name folders, and files and folders in any name folder
  3. name/ -> all files and folders in any name folder
  4. name.file -> all files with the name.file
  5. *.file -> all files withe .file extension

`SSH`: SSH is a secure shell network protocol that is used for network management, remote file transfer, and remote
system access. SSH uses a pair of SSH keys to establish an authenticated and encrypted secure network protocol. It
allows for secure remote communication on unsecured open networks.

### Codes

* `touch .gitignore`: create a .gitignore file
* generating an SSH key pair:

    1. `ssh-keygen -t rsa -b 4096 -C "<your email>"`
    2. `ssh-add /Users/user/.ssh/id_rsa`

* use SSH in GitHub:

    1. `clip < /Users/user/.ssh/id_rsa.pub` -> copy the key to your clipboard
    2. add SSH key on GitHub setting
    3. `ssh -T <your email>` -> test SSH connection
    4. `git remote add ssh-origin <repository SSH URL>` -> add a new origin by SSH
    5. `git remote set-url origin <repository SSH URL>` -> change a remote origin from HTTPS to SSH

## Note

```text
I will update this tutorial if I acquire any new information.
```

## Sources

```text
www.w3schools.com
CloudStudio.com.au
```
