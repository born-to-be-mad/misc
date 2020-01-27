## Terminology
* *Git* - an open source program for tracking changes in text files, and is the core technology that GitHub, the social and user interface, is built on top of.
* *Branch* - a parallel version of a repository. It is contained within the repository, but does not affect the primary or master branch allowing you to work freely without disrupting the "live" version. 
 
## GIT Popular commands

#### git config
It configures user data which will be used with your commits.

Configure user name: `git config –global user.name “[name]”`

Configure user e-mail: `git config –global user.email “[email address]”`  

#### git init
It is used to start a new repository.

Usage: `git init [repository name]`

#### git clone
It is used to obtain a repository from an existing URL.

Usage: `git clone [url]`

 
#### git add
It adds file(s)/directory(s) to the staging area.

Add one file: `git add [file]`

Add all files:`git add -A` or `git add *`
  
#### git commit
* Record or snapshot the file permanently in the version history: 
```
git commit -m “[ Type in the commit message]”
```
* Commits any files you’ve added with the git add command and also commits any files you’ve changed since then:
```
git commit -a
```
  
#### git diff
* `git diff` shows the file differences which are not yet staged.
* `git diff –staged` shows the file differences between the files in the staging area and the latest version present.
* `git diff [first branch] [second branch]` shows the differences between the two branches mentioned.

#### git reset
* `git reset [file]` unstages the file, but it preserves the file contents.
* `git reset [commit]` undoes all the commits after the specified commit and preserves the changes locally.
* `git reset –hard [commit]` discards all history and goes back to the specified commi

#### git status
`git status` lists all the files that have to be committed.

#### git rm
`git rm [file]` deletes the file from your working directory and stages the deletion.

#### git log
* `git log` is used to list the version history for the current branch
* `git log –follow[file]` lists version history for a file, including the renaming of files also.

#### git show
`git show [commit]` shows the metadata and content changes of the specified commit.

#### git tag
`git tag [commitID]` is used to give tags to the specified commit.

#### git branch
* `git branch` lists all the local branches in the current repository.
* `git branch [branch name]` creates a new feature branch.
* `git branch -d [branch name]` deletes the feature branch.

#### git checkout
`git checkout [branch name]` is used to switch from one branch to another.
`git checkout -b [branch name]` creates a new branch and also switches to it.

#### git merge
`git merge [branch name]` merges the specified branch’s history into the current branch.

#### git remote
`git remote add [variable name] [Remote Server Link]` is used to connect your local repository to the remote server.

#### git push
* `git push [variable name] master` sends the committed changes of master branch to your remote repository.
* `git push [variable name] [branch]` sends the branch commits to your remote repository.
* `git push –all [variable name]` pushes all branches to your remote repository.
* `git push –all [variable name] :[branch name]` deletes a branch on your remote repository.

#### git pull
`git pull [Repository Link]` fetches and merges changes on the remote server to your working directory.

#### git stash
`git stash save` temporarily stores all the modified tracked files.
`git stash pop` restores the most recently stashed files.
`git stash list` lists all stashed changesets.
`git stash drop` discards the most recently stashed changeset.
 
 
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
