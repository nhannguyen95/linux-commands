## Navigation

`pwd` - print working directory

`cd`

## Exploring the system

`ls`

`file`

`less` - g, G, /characters, n

## Permissions

`id`

`chmod`

effective user ID, effective group ID, sticky bit

`umask`

`su` - switch user

`sudo` - can be configured to allow an ordinary user to execute commands as a different user (usually the superuser) in a controlled way (to see what privileges are granted by sudo, use `-l` option)

`chown` - change file owner and group. Superuser privileges are required to use this command.

`passwd`

## Redirection

By default, stdin is attached to keyboard, stdout and stderr are linked to the screen at not saved into disk file.

I/O redirection allows us to change where into comes from and where output goes.

`>` - redirection operator:
  - `> filename`
  - `>>` - append the result instead of truncating like `>`
  - `2>` - redirect stderr
  - `&>` or `&>>`: both
  - `2> /dev/null`: throw away the error messages

`|`: std output of one command can be pipped into the std input of another

`cat` - concatenate files: reads >= 1 files and copies them to stdout:
  - is often used to display short text files.
  - `cat` with no arguments copies from stdin.

`sort` - sort lines of text

`uniq` - report or omit repeated lines: accepts a sorted list of data from either stdin or a single filename argument, removes any duplicates from the list:
  - `d` flag to see the list of duplicates instead.
 
`wc` - display #lines, #words and #bytes in files:
  - `l` flag to only report #lines.
 
`grep` - print LINES matching a pattern
  - usage: `grep pattern [file...]`
  - `i` flag to ignore case
  - `v` flat to print lines that do not match the pattern
  
`head` - print first few lines of a file

`tail` - print last few lines of a file
  - `-f` flat to monitor files in real time.

`tee` - read from stdin and output to stdout AND files
