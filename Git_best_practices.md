# Terminology

- _Git_ - an open source program for tracking changes in text files, and is the core technology that GitHub, the social and user interface, is built on top of.
- _Branch_ - a parallel version of a repository. It is contained within the repository, but does not affect the primary or master branch allowing you to work freely without disrupting the "live" version.

# How to Write a Git Commit Message (!)

## The seven rules of a great Git commit message

- Separate subject from body with a blank line
- Limit the subject line to 50 characters
- Capitalize the subject line
- Do not end the subject line with a period
- Use the imperative mood in the subject line
- Wrap the body at 72 characters
- Use the body to explain what and why vs. how

* https://chris.beams.io/posts/git-commit/

# Oh Shit, Git!?!

- https://ohshitgit.com/
- [Как это отменить?! Git-команды для исправления своих ошибок](https://tproger.ru/translations/problems-with-git/)
- [Полезные команды Git: безопасная отмена коммитов, добавление файла из другой ветки и другие](https://tproger.ru/translations/git-tips-and-tricks/)

# GIT Tips and Tricks

# GIT MUST-HAVE ALIASES

## How to configure aliases

`git config alias.ALIAS_SHORT_NAME ALIAS_CONTENT`- add locally
`git config --global alias.ALIAS_SHORT_NAME ALIAS_CONTENT`- add globally
F.e. `git config --global alias.st status` -> `git st` = `git status`

`git config alias.qm "!git checkout $1; git merge @{-1}"` alias with parameters.

`git status`, `git add`, `git commit`, and `git checkout` are common commands, so it is a good idea to have abbreviations for them.


Git aliases can be configured via section '[alias]'.
Add the following to the `.gitconfig` file in your \$HOME directory.
```batch
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  cfgg = config -e --global
  cfgl = config -e --local
  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  hist1 = log --all --decorate --oneline --graph
  hist2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
  type = cat-file -t
  dump = cat-file -p
  stat = shortlog -nse
  lg = log --pretty='%Cred%h%Creset | %C(yellow)%d%Creset %s %Cgreen(%cr)%Creset %C(cyan)[%an]%Creset' --graph
  so = show --pretty='parent %Cred%h%Creset commit %Cred%h%Creset%C(yellow)%d%Creset %n%n%w(72,2,2)%s%n%n%w(72,0,0)%C(cyan)%an%Creset %Cgreen%ar%Creset'
  undo = reset --soft HEAD~1
  amend = !git log -n 1 --pretty=tformat:%s%n%n%b | git commit -F - --amend
  hide = update-index –-skip-worktree
  unhide = update-index –-no-skip-worktree
  unhide-all = ls-files -v | grep -i ^S | cut -c 3- | xargs git update-index –-no-skip-worktree
  hidden = ! git ls-files -v | grep ‘^S’ | cut -c3-
  tree = log --graph --pretty=format:'%C(yellow)%h%C(cyan)%d%Creset %s %C(white)- %an, %ar%Creset'
  review= "!f() { git fetch origin pull/$1/head:pr/$1 && git checkout pr/$1; }; f"
  trim = !git branch --merged | grep -v '*' | xargs -n 1 git branch -d
```

#### Profile aliases

If your shell supports aliases, or shortcuts, you can add aliases on this level too(FILE.profile):

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

## Top aliases
* The `git undo` alias is probably my most-used one, as it “undoes” the last commit and gives you a bit of a do-over to make changes, 
  unstage files, and fix a recently screwed up commit.
```
undo = reset --soft HEAD~1
```  

* The `git amend` alias allows to add any staged changes to the previous commit without having to update the commit message.
```
amend = !git log -n 1 --pretty=tformat:%s%n%n%b | git commit -F - --amend
```  

* The `git tree` alias allows to see what has been merged into the current branch, and when, 
which can make it significantly easier to get a larger view of the activity within a given project.
```
tree = log --graph --pretty=format:'%C(yellow)%h%C(cyan)%d%Creset %s %C(white)- %an, %ar%Creset'
```  

* The `git review` alias allows to checkout a pull request by its ID, which I can then run through the ringer and validate without having to jump through any hoops..
```
review= "!f() { git fetch origin pull/$1/head:pr/$1 && git checkout pr/$1; }; f"
```  

* The `git trim` alias gets a list of all of the branches that have been merged into the current branch, and deletes them from your local repository. 
This is super useful when pulling down a large number of feature branches, as you can clean them up as they get merged without much overhead.
```
trim = !git branch --merged | grep -v '*' | xargs -n 1 git branch -d
```  


# GIT Popular commands
#### git rerere («reuse recorded resolution»)
Allows reusing recorded resolution of conflicted merges. We can automate the conflict resolution. 
`git config --global rerere.enabled true` to activate globally.
`git config --global rerere.autoupdate true` if we need automatically index corrected files.

[Details](https://git-scm.com/docs/git-rerere)

#### git config

Better to configure all properties by editing config file `git config --global -e`. 

It configures user data which will be used with your commits.

Configure user name: `git config –global user.name “[name]”`

Configure user e-mail: `git config –global user.email “[email address]”`

Configure git editor for Windows:
```batch
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```
Configure git editor on Linux/Mac:`git config --global core.editor "atom --wait"`

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
* `git commit --amend --no-edit` to modify the Previous Commit Without Changing the Commit Message
* `git add -p <filename>` you can choose which parts of code from a file you want to include in your commit. After running the command you will get the list of the options you can add to Git: `add -p`.
* `git reflog` to get the record of all the commits done in Git.
   Then `git reset HEAD@{index}` or `git reset --soft` or `git reset --hard` 
* `git checkout --conflict=diff3 <filename>` to comparing two conflicting versions, inc. the base version.
  `git config --global merge.conflictstyle diff3` to set default
* `git config --global help.autocorrect <integer>` The integer value represents a tenth of a second.

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

### Standard workflow

- create a new local branch 'feature' via command `git checkout -b feature`

  > > This command creates a new branch, named "feature", and makes that branch our active branch.

- code changes, commits and etc. 'git add', 'git push'...

- switch back to the 'master' branch `git checkout master`

- get latest changes from the remote repository via `git pull origin master`

- merge the 'feature' branch into 'master'(LOCAL) via `git merge feature`

- delete the 'feature` branch via 'git branch -d feature'

- push changes to remote master via `git push origin master`

## Cherry-picking

* `git cherry-pick <commit-hash>` to cherry-pick a commit from another branch.
* `git cherry-pick -n <commit-hash>` to cherry-pick the commit but it won’t commit the changes. It will only stage all the changes.
* `git cherry-pick -continue` or `git cherry-pick -abort` when you face conflicts while cherry-picking.
* `git cherry-pick -m` to mention the parent branch number when you are cherry-picking a merge commit.
* `git cherry-pick A..B` to cherry-pick a series of commits from A(not included) to B.
* `git cherry-pick A^..B` to cherry-pick a series of commits from A(included) to B.

## Fetching
* `git fetch` to download all the remote changes to local without affecting your flow.
* 'git fetch --all' to fetch all remotes
* `git diff <branch_name> origin/<branch_name>` - to know the remote changes. 
  Remember that all the changes from the second branch are shown and the changes from the first branch are omitted. 
  So that you can see the difference between the two branches.
* `git diff develop origin/develop —stat` -  to show only the files changed in the local and remote branches.
* `git log develop..origin/develop` - to see all the commits from origin/develop but that are not present in the develop branch. 
* In this way, you can know that how many new commits are added to the remote develop branch that is not present in the local branch.
* `git log origin/develop..develop` - to see all commits from develop (local) but commits that are not present in origin/develop (remote).
* `git pull` = `git fetch` + `git merge`
* `git pull origin develop` - only fetches the remote changes of develop branch and not other branches. And it also merges the remote changes to the branch.
* `git pull —rebase` if we want to rebase after fetching,cause by default, `git pull` will execute `git merge`.


# Materials
- [Как склеить коммиты и зачем это нужно](https://htmlacademy.ru/blog/boost/tools/how-to-squash-commits-and-why-it-is-needed)
