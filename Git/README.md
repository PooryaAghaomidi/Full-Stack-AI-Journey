# Git tutorial

Git is a distributed version control system that tracks versions of files. It is often used to control source code by programmers collaboratively developing software.

Download and install `git` from the official website: https://git-scm.com

Then you can run git commands on your command shell (e.g. git bash, cmd, powershell, etc.)


## Table of Contents

- [Section One: Git](#section-one-git)
- [Section Two: GitHub](#section-two-github)
- [Section Three: Advanced](#section-three-advanced)
- [Section Four: Undo](#section-four-undo)


## Section One: Git

* `git --version`: get version
* `git config --global user.name "<your username>"`: set username (use global to set the username and e-mail for every repository)
* `git config --global user.email "<your email>"`: set email
* `git config --list`: list configuration
* `git init`: initialize a git repository in the current folder (git creates a hidden folder to keep track of changes)
* `git status`: display information about the status of that repository
* `git status --short`: display information in a more compact way
* `git add <your file>`: add that file to the staging environment (staged files are files that are ready to be committed to the repository)
* `git add -A`: add all files to the staging environment
* `git commit -m "<your message>"`: move from stage to commit (adding commits keep track of our progress and changes as we work)
* `git commit -m .`: commit without a message
* `git log`: view the history of commits for a repository
* `git <command> -help`: help remembering the specific option for a command
* `git help --all`: list all possible commands
* `git branch <branch name>`: create a new branch (a branch is a separate version of the main repository)
* `git branch`: list all branches and master (master/main is the primary branch of a repository)
* `git branch -d <branch name>`: delete the branch
* `git checkout <branch name>`: moving from the current branch to the one specified (changes the local drive so that it reflects the destination branch)
* `git merge <branch name>`: merge master with the branch (solve conflicts if necessary)
* `git tag`: list all tags (versions) in the repository
* `git tag -a <your version> -m "<your message>`: assign a version to the current HEAD with an optional message (HEAD is the current commit)
* `git push origin <your version>`: push a version to the remote repository
* `git tag -d <your version>`: delete a version
* `git checkout <your version>`: moving from the current branch to the version
* `git tag <your version> <commit hash>`: assign a version to a specific commit


## Section Two: GitHub


## Section Three: Advanced


## Section Four: Undo


## Sources

```text
www.w3schools.com
```
