## Terminology
* *Git* - an open source program for tracking changes in text files, and is the core technology that GitHub, the social and user interface, is built on top of.
* *Branch* - a parallel version of a repository. It is contained within the repository, but does not affect the primary or master branch allowing you to work freely without disrupting the "live" version. 
 
## GIT Popular commands
#### git config
Configure user name: `git config –global user.name “[name]”`
Configure user e-mail: `git config –global user.email “[email address]”`  
It sets the author name and email address respectively to be used with your commits.

#### git init
#### git clone
#### git add
#### git commit
#### git diff
#### git reset
#### git status
#### git rm
#### git log
#### git show
#### git tag
#### git branch
#### git checkout
#### git merge
#### git remote
#### git push
#### git pull
#### git stash
 
## Feature branching
* check branches `git branch`.
If there are no branches, the result is:
```
* master
```
* create a new branch `git checkout -b feature-branch`. <br />This command does two things:
  * it creates a new local metrics branch
  * it switches the working folder to reference the newly created branch<br />
Check the branches via `git branch`
```
* feature-branch
 master
```
