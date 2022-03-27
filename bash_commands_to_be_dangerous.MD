# 3Linux commands

* `killall -I notes`  kills the matching process by name(case insensitive.
* `Ctrl + x + e` will open an editor where you can type your command. And upon saving the editor, the command will run
  on the terminal.
* `touch a` to create an empty file 'a'.
* `touch -r file_name2 file_name1`  to copy the timestamp from another file.
* `tee` is command in UNIX is a command-line utility for copying standard input to standard output

## Must-know commands

- `grep` - search by template

    - `grep "smth" file` - search 'smth' in file
    - `grep -i "smth" file` - search 'smth' case-insensitive
    - `grep -c "smth" file` - count search results of 'smth'

- `ls` - list directories and files

- `pwd` - show full system path of current directory

- `cat` - view, concat, create new files(with content)

    - read file content `cat file`
    - redirect the output of one file to another file `cat somefile > somefile2`

- `echo` - view smth, f.e. environment variable and etc

    - `echo "some text"`

- `touch` - create empty file

    - `touch somefile`
    - `cat` creates a file with content, but `touch` create an empty file

- `mkdir` - creates an empty directory in the current path

    - `mkdir some-directory` - creates an empty 'some-directory'

- `rm` - removes the path(file or directory)
    - `rm someFile` - removes 'someFile'
    - `rm -rf some-directory` - removes 'some-directory' with the content

- `rmdir` - removes a directory

    - `rmdir some-directory`

- `tail` - read a file from the end(tail)

    - `tail somefile` - reads last 10 lines from 'someFile'
    - `tail -n 20 somefile` - reads last 20 lines from 'someFile'

- `wget` - GNU `Wget` loads files via HTTP, HTTPS, FTP and FTPS.

    - `wget someurl` gets data from 'someurl'

- `find` - searches for a file or a directory

    - `find path -name filename`
    - `find . -name filename`- searches all files from current path with the name 'filename'
    - `find components -name "*.js"` - searches for file wih the extension ".js" in the directory 'components'

- `mv` - moves files/directories

    - `mv somefile /to/some/other/path`
    -
        - `mv somedirectory /to/some/other/path`

- `cal` - shows current month in console

- `Ctrl + A/Ctrl + E` - move the cursor to the start/end of the line.

- `Ctrl + U` - delete all characters before the cursor (a great alternative to spamming backspace whenever you mistype
  your password).

- `Ctrl + R` - search through your command history.

## Utilities

-`pstree -T` shows a nice and clean overview of processes running on your system.

- `nmap` - finds open ports on some system

```batch
nmap -p 1-65535 my.hostname.com     # Scan whole ports range
nmap -p 80,8080,443 my.hostname.com # Scan 80,8080,443 
nmap --top-ports 10 my.hostname.com # Scan top 10 portsnc -zvw3 my.hostname.com 587        # Check if port 587 is open
netstat -tlpn                       # List open local ports
```

## Useful command line samples

- `!$` – The ‘Last Argument’. It substitutes in the last argument of the last command into your line.

- `!:2` – The ‘nth Argument’. you can use this to re-use specific arguments from the last command rather than all of
  them.

- `!:1-$` – The ‘All The Arguments’. shortcut to ask for all the arguments to the previous command from the second one (
  remember they’re zero-indexed) to the last one (represented by the \$ sign).

- `!-2:$` – The ‘Last But n‘ One. -n: (where n is the number of commands to go back in the history) after the ! to grab
  the last argument from an older command

- `!$:h` – The ‘Get Me The Folder’ One. Get the last argument to the last command, and take off its last filename
  component, leaving only the folder part.

- `!#:1` – The ‘The Current Line’ One. It is esy to create backup files `cp /path/to/some/file !#:1.bak`

- `!!:gs` – The ‘Search and Replace’ One. It searches across the referenced command, and replaces what’s in the first
  two / characters with what’s in the second two. F.e. `!!:gs/does/did/`

Test

```
ping !#:0:gs/i/o
vi /tmp/!:0.txt
ls !$:h
cd !-2:h
touch !$!-3:$ !! !$.txt
cat !:1-$
```

# Delete node modules

* This will spit out a list of all of the `node_modules` that it finds, and how much disk space they’re taking up (
  individually and in total).

```
# Mac/Linux
find . -name "node_modules" -type d -prune -print | xargs du -chs

# Windows
FOR /d /r . %d in (node_modules) DO @IF EXIST "%d" echo %d"
```

* Actually deleting files

```
# Mac/Linux
find . -name 'node_modules' -type d -prune -print -exec rm -rf '{}' \;

# Windows
FOR /d /r . %d in (node_modules) DO @IF EXIST "%d" rm -rf "%d"
```

## Miscellaneous

* random user password `openssl rand -base64 32`
```bash
USERNAME=azureuser
PASSWORD=$(openssl rand -base64 32)
```