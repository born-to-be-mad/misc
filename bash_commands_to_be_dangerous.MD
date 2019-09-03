* `!$` – The ‘Last Argument’. It substitutes in the last argument of the last command into your line.

* `!:2` – The ‘nth Argument’. you can use this to re-use specific arguments from the last command rather than all of them.

* `!:1-$` – The ‘All The Arguments’. shortcut to ask for all the arguments to the previous command from the second one (remember they’re zero-indexed) to the last one (represented by the $ sign).

* `!-2:$` – The ‘Last But n‘ One. -n: (where n is the number of commands to go back in the history) after the ! to grab the last argument from an older command

* `!$:h` – The ‘Get Me The Folder’ One. Get the last argument to the last command, and take off its last filename component, leaving only the folder part.

* `!#:1` – The ‘The Current Line’ One. It is esy to create backup files `cp /path/to/some/file !#:1.bak`

* `!!:gs` – The ‘Search and Replace’ One. It searches across the referenced command, and replaces what’s in the first two / characters with what’s in the second two. F.e. `!!:gs/does/did/`

Test
```
ping !#:0:gs/i/o
vi /tmp/!:0.txt
ls !$:h
cd !-2:h
touch !$!-3:$ !! !$.txt
cat !:1-$
```
