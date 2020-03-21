## Must-know commands

- grep - search by template

  - `grep "smth" file` - search 'smth' in file
  - `grep -i "smth" file` - search 'smth' case-insensitive
  - `grep -c "smth" file` - count search results of 'smth'

- ls - list directories and files

- pwd - show full system path of current directory

- cat - view, concat, create new files(with content)

  - read file content `cat file`
  - redirect the outpput of one file to another file `cat somefile > somefile2`

- echo - view smth, f.e. environment variable and etc

  - `echo "some text"`

- touch - create empty file

  - `touch somefile`
  - `cat` creates a file with content, but `touch` create an empty file

- mkdir - creates an empty directory in the current path

  - `mkdir some-directory` - creates an empty 'some-directory'

- rm - removes the path(file or directory)
  - `rm someFile` - removes 'someFile'
  - `rm -rf some-directory` - removes 'some-directory' with the content
- rmdir - removes a directory

  - `rmdir some-directory`

- tail - read fiel from the end(tail)

  - `tail somefile` - reads last 10 lines from 'someFile'
  - `tail -n 20 somefile` - reads last 20 lines from 'someFile'

- wget - GNU `Wget` loads files via HTTP, HTTPS, FTP and FTPS.

  - `wget someurl` gets data from 'someurl'

- find - searches for file or directory

  - `find path -name filename`
  - `find . -name filename`- searches all files from current path with the name 'filename'
  - `find components -name "*.js"` - searches for file wih the extension ".js" in the directry 'components'

- mv - moves files/directories

  - `mv somefile /to/some/other/path`
  - - `mv somedirectory /to/some/other/path`

- cal - shows current month in console

## Usefull command line samples

- `!$` – The ‘Last Argument’. It substitutes in the last argument of the last command into your line.

- `!:2` – The ‘nth Argument’. you can use this to re-use specific arguments from the last command rather than all of them.

- `!:1-$` – The ‘All The Arguments’. shortcut to ask for all the arguments to the previous command from the second one (remember they’re zero-indexed) to the last one (represented by the \$ sign).

- `!-2:$` – The ‘Last But n‘ One. -n: (where n is the number of commands to go back in the history) after the ! to grab the last argument from an older command

- `!$:h` – The ‘Get Me The Folder’ One. Get the last argument to the last command, and take off its last filename component, leaving only the folder part.

- `!#:1` – The ‘The Current Line’ One. It is esy to create backup files `cp /path/to/some/file !#:1.bak`

- `!!:gs` – The ‘Search and Replace’ One. It searches across the referenced command, and replaces what’s in the first two / characters with what’s in the second two. F.e. `!!:gs/does/did/`

Test

```
ping !#:0:gs/i/o
vi /tmp/!:0.txt
ls !$:h
cd !-2:h
touch !$!-3:$ !! !$.txt
cat !:1-$
```
