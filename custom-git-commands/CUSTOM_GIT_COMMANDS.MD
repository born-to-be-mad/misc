# Hot to configure custom git commands
* create folder `mkdir my-custom-git-commands`
* add custom commands to $PATH `export PATH=$PATH:/BASIC_PATH/my-custom-git-commands`
* make very file inside `my-custom-git-commands` executable by `chmod +x git-lazypush`

# Description of existing custom commands
* `git-lazypush`- the custom command to add all files, commit with the message passed as the parameter and psu to the remote server.
* `git-switch-to`- the custom command to checkout to a new branch with all the unstaged changes present in the current branch.
* `git-remote-diff` - the custom command to view the difference between the local and the remote of the specified branch.
* `git-remote-log` - the custom command helps you to view the commit logs between the local and remote changes of the given branch.
* `git-hard-delete` - the custom command to delete a branch both locally and remotely.
* `git-lazypr` - the idea(not yet implemented) for custom command to create a pull request. There are APIs available in Github, Gitlab to create a PR in a repo. 
