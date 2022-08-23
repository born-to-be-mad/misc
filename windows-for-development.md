# ALIASES

## Aliases in Git Bash

* Open your `aliases.sh` in you Git folder(default `/c/'Program Files'/Git/etc/profile.d`)
* Add necessary aliases by following the syntax `alias x='y'`, where `x` is the alias to the `y` command.

### Useful aliases

* `alias g='git'` to use git commands without the `git` prefix
* `alias k='kubectl`` to use kubectl commands without the `kubectl` prefix
* `alias cll='clear; ls -lah'` to clear thew view and list all files in current directory
* `alias countFiles='ls -1 | wc -l'` to count the number of files in the current directory
* `alias ll='ls -lah'` to list all files in current directory
* `alias ls='ls -F --color=auto --show-control-chars'` to list all files in current directory with colors and control
  characters

## Aliases in Windows Command Prompt

The easiest way is to add bat-references available on the PATH.

* Call `kubect` via `k` alias
  ** create `k.bat`

```
@echo off
echo.
kubectl.exe %*
``` 

* put this file into the folder which is available on the PATH (any files in it will be found every time), f.e. `C:\BIN`
  or `C:\ALIASES`