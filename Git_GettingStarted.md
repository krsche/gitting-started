# Getting Started with Git <!-- omit in toc -->

## Table of Contents
- [1. General](#1-general)
  - [1.1 Installation](#11-installation)
    - [1.1.1 Git](#111-git)
    - [1.1.2 VisualStudio Code](#112-visualstudio-code)
  - [1.2 References](#12-references)
    - [1.2.1 Git Cheatsheet](#121-git-cheatsheet)
    - [1.2.2 Visualizing Git](#122-visualizing-git)
    - [1.2.3 GitFlow](#123-gitflow)
    - [1.2.4 GitHub](#124-github)
- [2. Follow Along](#2-follow-along)
  - [2.1 Prerequisites](#21-prerequisites)
  - [2.2 Configuring Git](#22-configuring-git)
  - [2.3 Creating a local repository](#23-creating-a-local-repository)
  - [2.4 Adding Files](#24-adding-files)
  - [2.5 Reviewing changes before commiting](#25-reviewing-changes-before-commiting)
  - [2.6 Setting up git-aliases](#26-setting-up-git-aliases)
  - [2.7 Using branches](#27-using-branches)
  - [2.8 Navigating the History](#28-navigating-the-history)
  - [2.9 Merging](#29-merging)
  - [2.10 Git remotes](#210-git-remotes)

___

# 1. General
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


## 1.2 References
### 1.2.1 Git Cheatsheet
https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf

### 1.2.2 Visualizing Git
http://git-school.github.io/visualizing-git/#free-remote

### 1.2.3 GitFlow
https://www.bluesource.at/fileadmin/user_upload/bluesource/Wissen/Detailseite/git-model.jpg

### 1.2.4 GitHub
https://github.com  
**GitHub Education Sponsoring**  
https://education.github.com/



# 2. Follow Along
## 2.1 Prerequisites
* Git is installed (make sure the git_bash is installed aswell)
* VSCode is installed

## 2.2 Configuring Git  
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

## 2.3 Creating a local repository
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

## 2.4 Adding Files
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

## 2.5 Reviewing changes before commiting
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

## 2.6 Setting up git-aliases
__!!! This step is optional, but in !!!__  
Since we're using some git commands a lot and we don't want to get tired of them let's set up some shorthands using git-aliases. : )  

Executing the command below sets the following aliases for us:  

| Shorthand               | Command description                                                                       |
| ----------------------- | ----------------------------------------------------------------------------------------- |
| __git s__               | git status                                                                                |
| __git df *\<id\>*__     | show files which were changed in the commit with id...                                    |
| __git tree__            | shows diagram of branches with commits visually in a tree (add --all to see all branches) |
| __git l__               | shows the last commits on this branch history                                             |
| __git co *\<branch\>*__ | git checkout                                                                              |
| __git ci__              | git commit                                                                                |
| __git br__              | git branch                                                                                |
| __git a__               | git add                                                                                   |
| __git d__               | git difftool                                                                              |


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
```
Go ahead and try some of the commands now!

## 2.7 Using branches
Go ahead and have a look at the website from __[1.2.2 Visualizing Git](#1.2.2-visualizing-git)__

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



## 2.8 Navigating the History
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

## 2.9 Merging
Merging can get tricky. Here is a simple example. We're merging the feature branch back into our develop branch. There are no conflicts because we we're working on different sections/files.

```bash
git checkout develop
git merge feature --no-ff --no-edit
git tree --all
```

__--> Now try to merge the develop branch back into our master branch__



## 2.10 Git remotes

Git remotes are the git servers we're using.
You can think of it as another repository where you and your colleagues work on together.

![Git Local-Remote repository](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR-xeH0cVulHlOPWX_29FCi6k5jDIO-ffy8ETkxueIVYJb99g5pew)

First of all, lets create a remote repository somewhere.
Let's use GitHub for now. Go to the website referenced in [1.2.4 GitHub](1.2.4-github) and create a account using your Email-Address

When you're logged in, __create a new private repository__ for our tutorial and name it __*hse_git_tutorial*__

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