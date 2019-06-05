# Getting Started with Git <!-- omit in toc -->

> Git your code together! :)

## Table of Contents
- [1. General](#1-general)
  - [1.1 Installation](#11-installation)
    - [1.1.1 Git](#111-git)
    - [1.1.2 VisualStudio Code](#112-visualstudio-code)
    - [1.1.3 (optional) BeyondCompare](#113-optional-beyondcompare)
  - [1.2 References](#12-references)
    - [1.2.1 Git SCM Documentation / Tutorials](#121-git-scm-documentation--tutorials)
    - [1.2.2 Git Cheatsheet](#122-git-cheatsheet)
    - [1.2.3 Visualizing Git](#123-visualizing-git)
    - [1.2.4 GitFlow](#124-gitflow)
    - [1.2.5 GitHub](#125-github)
- [2. Showcase](#2-showcase)
- [3. Follow Along](#3-follow-along)
  - [3.1 Prerequisites](#31-prerequisites)
  - [3.2 Configuring Git](#32-configuring-git)
  - [3.3 Creating a local repository](#33-creating-a-local-repository)
  - [3.4 Adding Files](#34-adding-files)
  - [3.5 Reviewing changes before commiting](#35-reviewing-changes-before-commiting)
  - [3.6 Setting up git-aliases](#36-setting-up-git-aliases)
  - [3.7 Using branches](#37-using-branches)
  - [3.8 Navigating the History](#38-navigating-the-history)
  - [3.9 Merging](#39-merging)
  - [3.10 Git remotes](#310-git-remotes)
  - [3.11 Authenticating using ssh](#311-authenticating-using-ssh)
    - [3.11.1 Concept](#3111-concept)
    - [3.11.2 Setup](#3112-setup)
  - [3.12 Add a git remote](#312-add-a-git-remote)

___

# 1. General

From https://git-scm.com/ :
> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.  

__Git-Handbook__  
https://guides.github.com/introduction/git-handbook/


## 1.1 Installation
### 1.1.1 Git
__UBUNTU:__  
`sudo apt-get install git`  
__WINDOWS:__  
https://git-scm.com/download/win

### 1.1.2 VisualStudio Code
__UBUNTU:__  
`wget -O vscode.deb https://code.visualstudio.com/docs/?dv=linux64_deb && sudo apt install vscode.deb`  
__WINDOWS:__  
https://code.visualstudio.com/download

### 1.1.3 (optional) BeyondCompare
https://www.scootersoftware.com/download.php

## 1.2 References
### 1.2.1 Git SCM Documentation / Tutorials
https://git-scm.com/doc

### 1.2.2 Git Cheatsheet
https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf

### 1.2.3 Visualizing Git
http://git-school.github.io/visualizing-git/#free-remote

### 1.2.4 GitFlow
https://www.bluesource.at/fileadmin/user_upload/bluesource/Wissen/Detailseite/git-model.jpg

### 1.2.5 GitHub
https://github.com  
**GitHub Education Sponsoring**  
https://education.github.com/


# 2. Showcase
https://github.com/espressif/esp-idf

```bash
git clone --recursive -b master https://github.com/espressif/esp-idf.git
```

```bash
git gui
```


# 3. Follow Along
## 3.1 Prerequisites
* Git is installed (make sure the git_bash is installed aswell)
* VSCode is installed

## 3.2 Configuring Git  
If you're using Windows, replace the double quotes (") below with simple quotes (')
```bash
git config --global user.name 'John Doe'
git config --global user.email johndoe@example.com
git config --global color.ui auto
```

If you want to use vscode for showing file diffs and as the mergetool do this:
```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
```

If you have Beyond Compare 3 or 4 installed and want to use it instead of vscode use this:
```bash
# Use 'bc3' even if you have Beyond Compare 4!
git config --global diff.tool bc3
git config --global difftool.bc3.trustExitCode true
git config --global merge.tool bc3
git config --global mergetool.bc3.trustExitCode true
```

## 3.3 Creating a local repository
```bash
git init <foldername>
cd <foldername>
touch readme.md
git status
git add readme.md
git status
git commit -m "Initial Commit"
git status
```

## 3.4 Adding Files
```bash
echo "# This is a Test-Repository!" >> readme.md
cat readme.md
printf "import sys \\nprint(\"This is a very nice python test using python version: \" + str(sys.version_info[0]))" > pythonTest.py
git status
git add pythonTest.py
git status
git add readme.md
git status
git commit -m "added a nice python script"
```

## 3.5 Reviewing changes before commiting
```bash
printf "# This is a Test-Repository\nIt includes a very nice python script :)" > readme.md
git status
printf "import sys \\nprint(\"This is a great python test using python version: \" + str(sys.version_info[0]))" > pythonTest.py
git status
git diff
git difftool
git add *
git status
git commit -m "changed the very nice script to a great script"
git status
printf "# This is a Test-Repository\nIt includes a great python script :)" > readme.md
git difftool
git add *
git status
git commit --amend --no-edit
git status
git log
```

## 3.6 Setting up git-aliases
__!!! This step is optional, but in !!!__  
Since we're using some git commands a lot and we don't want to get tired of them let's set up some shorthands using git-aliases. : )  

Executing the command below sets the following aliases for us:  

| Shorthand               | Command description                                                                                       |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| __git s__               | git status                                                                                                |
| __git df *\<id\>*__     | show files which were changed in the commit with id...                                                    |
| __git tree__            | shows diagram of branches with commits visually in a tree (add --all to see all branches)                 |
| __git l__               | shows the last commits on this branch history                                                             |
| __git co *\<branch\>*__ | git checkout                                                                                              |
| __git ci__              | git commit                                                                                                |
| __git br__              | git branch                                                                                                |
| __git a__               | git add                                                                                                   |
| __git d__               | git difftool                                                                                              |
| __git dirdiff__         | compare the whole folder structure to the previous version (only available if BeyondCompare is installed) |


```bash
# Just copy and paste the whole thing :)
git config --global alias.s status &&\
git config --global alias.df "diff-tree --no-commit-id --name-only" &&\
git config --global alias.tree "log --graph --pretty=format:'%C(yellow)%h %Cred%ad %Cgreen%d %Creset%s' --date=short --abbrev-commit" &&\
git config --global alias.l "log --pretty=format:'%C(yellow)%h %Cred%ad %Cblue%an %Cgreen%d %Creset%s' --date=short" &&\
git config --global alias.co checkout &&\
git config --global alias.ci commit &&\
git config --global alias.br branch &&\
git config --global alias.a add &&\
git config --global alias.d difftool
git config --global alias.dirdiff "difftool --dir-diff --tool=bc --no-prompt"
```
Go ahead and try some of the commands now!

## 3.7 Using branches
Go ahead and have a look at the website from __[1.2.3 Visualizing Git](#123-visualizing-git)__

```bash
git branch
git branch develop
git branch
git checkout develop
git branch
printf "import sys \\nprint(\"This is a great python test using python version: \" + str(sys.version_info[0]))\\nprint(\"I like it :)\")" > pythonTest.py
git difftool
git add *
git commit -m "added a great feature"
git status
git log
git tree
git checkout master
cat pythonTest.py
git status
printf "# This is a Test-Repository\nIt includes a great python script, which i like :)" > readme.md
git status
git add *
git commit -m "updated the readme"
git status
git tree --all
```



## 3.8 Navigating the History
One of the real handy features of version control is that you can roll-back to an older version of your repository and do stuff there.
Let's look into that now...

__by the way:__  
*HEAD Pointer* --> the keyword HEAD in git always points to the commit which is currently checked out.

```bash
git checkout develop
printf "import sys \\nprint(\"This is a great python test using python version: \" + str(sys.version_info[0]))\\nprint(\"I like it <3\")" > pythonTest.py
git s
git co <commit_id_of_develops_direct_parent_commit>
git add *
git s
git commit -m "added a feature"
git s
git tree --all
git co <commit_id_of_develops_direct_parent_commit>
git branch feature
git co feature
git s
git tree --all
echo "print(\"this is another script...\")" > anotherScript.py
git add *
git s
git ci -m "added another script"
git tree --all

```

## 3.9 Merging
Merging can get tricky. Here is a simple example. We're merging the feature branch back into our develop branch. There are no conflicts because we we're working on different sections/files.

```bash
git checkout develop
git merge feature --no-ff --no-edit
git tree --all
```

__--> Now try to merge the develop branch back into our master branch__



## 3.10 Git remotes

Git remotes are the git servers we're using.
You can think of it as another repository where you and your colleagues work on together.

![Git Local-Remote repository](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR-xeH0cVulHlOPWX_29FCi6k5jDIO-ffy8ETkxueIVYJb99g5pew)

First of all, lets create a remote repository somewhere.
Let's use GitHub for now. Go to the website referenced in [1.2.5 GitHub](125-github) and create a account using your Email-Address

When you're logged in, __create a new private repository__ for our tutorial and name it __*hse_git_tutorial*__

## 3.11 Authenticating using ssh
We use ssh to authenticate us against the GitHub Server. This prevents your neighbor from pushing to your repo... :)  

### 3.11.1 Concept  
SSH generates a private and public key pair. The public key is used to encrypt data and you can share it with *everyone*. The private key on the other hand is used to decrypt data which has been encrypted using the corresponding public-key. It's like your password for decrypting the data.  
In addition to that, I highly recommend using a password to encrypt the private key.  
This way an attacker needs access to your private key AND your secret password to decrypt the data - or in our case, authenticate to the GitHub server.

### 3.11.2 Setup
__Create an SSH-keypair__  
https://help.github.com/en/enterprise/2.16/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

__Add the public key to your GitHub account__  
https://help.github.com/en/enterprise/2.16/user/articles/adding-a-new-ssh-key-to-your-github-account

__Test the connection__  
https://help.github.com/en/articles/testing-your-ssh-connection
```bash
ssh -T git@github.com
```

## 3.12 Add a git remote

Now we're adding this remote repository to our existing repo as a *remote* called *origin*
```bash
git remote add origin <url_to_repository>
```

To upload our develop branch to the repository we use `git push`  after we checked out develop.
Since this is the first time we're *pushing* this branch to our remote we need to tell git where to link it to. For this we use `--set-upstream origin develop` or short `-u origin develop`

```bash
git co develop
git push -u origin develop
git s
git tree --remotes
```