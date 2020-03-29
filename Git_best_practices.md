# Terminology

- _Git_ - an open source program for tracking changes in text files, and is the core technology that GitHub, the social and user interface, is built on top of.
- _Branch_ - a parallel version of a repository. It is contained within the repository, but does not affect the primary or master branch allowing you to work freely without disrupting the "live" version.

# GIT MUST-HAVE AlIASES

## Common aliases

#### For Windows users:

```
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
git config --global alias.type 'cat-file -t'
git config --global alias.dump 'cat-file -p'
```

#### For Unix/Mac users:

`git status`, `git add`, `git commit`, and `git checkout` are common commands so it is a good idea to have abbreviations for them.

Add the following to the `.gitconfig` file in your \$HOME directory.

```
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  type = cat-file -t
  dump = cat-file -p

  hide = update-index –-skip-worktree
  unhide = update-index –-no-skip-worktree
  unhide-all = ls-files -v | grep -i ^S | cut -c 3- | xargs git update-index –-no-skip-worktree
  hidden = ! git ls-files -v | grep ‘^S’ | cut -c3-
```

#### Profile aliases

If your shell supports aliases, or shortcuts, you can add aliases on this level, too. :
FILE: .profile

```
alias gs='git status '
alias ga='git add '
alias gb='git branch '
alias gc='git commit'
alias gd='git diff'
alias gco='git checkout '
alias gk='gitk --all&'
alias gx='gitx --all'

alias got='git '
alias get='git '
```

# GIT Popular commands

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

- Record or snapshot the file permanently in the version history:

```
git commit -m “[ Type in the commit message]”
```

- Commits any files you’ve added with the git add command and also commits any files you’ve changed since then:

```
git commit -a
```

#### git diff

- `git diff` shows the file differences which are not yet staged.
- `git diff –staged` shows the file differences between the files in the staging area and the latest version present.
- `git diff [first branch] [second branch]` shows the differences between the two branches mentioned.

#### git reset

- `git reset [file]` unstages the file, but it preserves the file contents.
- `git reset [commit]` undoes all the commits after the specified commit and preserves the changes locally.
- `git reset –hard [commit]` discards all history and goes back to the specified commi

#### git status

`git status` lists all the files that have to be committed.

#### git rm

`git rm [file]` deletes the file from your working directory and stages the deletion.

#### git log

- `git log` is used to list the version history for the current branch
- `git log –follow[file]` lists version history for a file, including the renaming of files also.

#### git show

`git show [commit]` shows the metadata and content changes of the specified commit.

#### git tag

`git tag [commitID]` is used to give tags to the specified commit.

#### git branch

- `git branch` lists all the local branches in the current repository.
- `git branch [branch name]` creates a new feature branch.
- `git branch -d [branch name]` deletes the feature branch.

#### git checkout

`git checkout [branch name]` is used to switch from one branch to another.
`git checkout -b [branch name]` creates a new branch and also switches to it.

#### git merge

`git merge [branch name]` merges the specified branch’s history into the current branch.

#### git remote

`git remote add [variable name] [Remote Server Link]` is used to connect your local repository to the remote server.

#### git push

- `git push [variable name] master` sends the committed changes of master branch to your remote repository.
- `git push [variable name] [branch]` sends the branch commits to your remote repository.
- `git push –all [variable name]` pushes all branches to your remote repository.
- `git push –all [variable name] :[branch name]` deletes a branch on your remote repository.

#### git pull

`git pull [Repository Link]` fetches and merges changes on the remote server to your working directory.

#### git stash

`git stash save` temporarily stores all the modified tracked files.
`git stash pop` restores the most recently stashed files.
`git stash list` lists all stashed changesets.
`git stash drop` discards the most recently stashed changeset.

# GIT Tips and Tricks

## Feature branching

- check branches `git branch`.
  If there are no branches, the result is:

```
* master
```

- create a new branch `git checkout -b feature-branch`. <br />This command does two things:
  - it creates a new local metrics branch
  - it switches the working folder to reference the newly created branch<br />
    Check the branches via `git branch`

```
* feature-branch
 master
```

## Hiding files from comit

- We have 2 files modified, result via `git status`<BR/>

```
Changes not staged for commit:

	modified:   public.txt
	modified:   secret.txt
```

- By running the command `git update-index --skip-worktree secret.txt` the file secret.txt disappears from the working area.

- By running the command `git update-index --no-skip-worktree secret.txt` the file secret.txt returns to the working area.

## Archive Your Repository

Use the following command:

```
git archive master –format=zip –output= ../name-of-file.zip
```

It stores all files and data in a single zip file rather than the .git directory.<BR/> This creates only a single snapshot omitting version control completely.

## Bundle Your Repository

The following command `git bundle create ../repo.bundler master` turns a repository into a single file. <BR/>>
This pushes the master branch to a remote branch only contained in a file instead of a repository.

An alternate way to do it is:

```
cd..

git clone repo.bundle repo-copy -b master

cd repo-copy

git log

cd.. /my-git-repo
```

## Stash Uncommitted Changes

When we want to undo adding a feature or any kind of added data temporarily, we can “stash” them temporarily.

Use the commands below:

```
git status
git stash
git status
```

And when you want to re-apply the changes you “stash”ed , use the command below:
`git stash apply`

# BEST PRACTICES

- _Commit often_. When we commit often, we keep our commits small and share our work more frequently. That makes it easier to avoid large merge conflicts.
- _Don’t commit unfinished work_. Break your feature’s code into small but working chunks. Once you finish a chunk, test it, then commit it. This work method prevents the potential conflicts created by merging large bodies of code all at once. At the same time, it ensures we don’t commit small snippets of non-working code.
- _Before you commit, test_. Don’t commit something until you’ve tested it. Shared code that isn’t tested can create a lot of headaches and lost time for an entire team.
- _Commit related changes_. Make your commits small, and confine them to directly related changes. When we fix two separate bugs, they should take the form of two different commits.
- _Write clear commit messages_. Include a single-sentence summary of your changes. After that, explain the motivation for the change, and how it’s different from the previous version.
- _Use branches_. Branches are an excellent tool to avoid confusion and keep different lines of development separate.
- _Agree on your workflow_. Your team should agree on a workflow before the project starts. Whether that’s based on topic-branches, git-flow, long-running branches, or some other workflow will depend on the project.

##Git Branching

### Good links

- [Using branches](https://www.atlassian.com/git/tutorials/using-branches)

### Standart workflow

- create a new local branch 'feature' via command `git checkout -b feature`

  > > This command creates a new branch, named "feature", and makes that branch our active branch.

- code changes, commits and etc. 'git add', 'git push'...

- switch back to the 'master' branch `git checkout master`

- get latest changes from the remote repository via `git pull origin master`

- merge the 'feature' branch into 'master'(LOCAL) via `git merge feature`

- delete the 'feature` branch via 'git branch -d feature'

- push changes to remote master via `git push origin master`
