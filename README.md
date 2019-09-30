## What is the shell?

`date`

`cal` - displays current month’s calendar by default

`exit` - end terminal session

## Navigation

`pwd` - print working directory

`cd`

## Exploring the system

`ls`

`file`

`less` - g, G, /characters, n

## Manipulating files and directories

wildcards (blobbing)
* match any characterS
? match any single character
[chars] match any character that is a member of the set chars
[!chars] match any character that is not a member of the set chars
[[:class:]] match any character that is a member of the specified class

Most commonly used class:
[:alnum:]
[:alpha:]
[:digit:]
[:lower:]
[:upper:]

`cp`
- cp file1 file2
- cp item… dir
- cp -r dir1 dir2: result is dir2/dir1
- -a (—archive): copy files, directories and all of their attributes (ownerships, permissions..)

  -i (—interactive): prompt user for overwriting files
  
  -r (—recursive): recursively copy dirs and their contents
  
  -u (—update): only copy files that either don’t exit or newer than existing file in the destination dir
  
  -v: verbose
  
`mv`
- same usage as cp, except:
  
  mv dir1 dir2: change name of dir1 to dir2 if dir2 doesn’t exist, otherwise move dir1 inside dir2

`mkdir dir...`

`rm item…`
- item = file or dir
- rm -rf file1 dir1: either file1 or dir1 do not exist, rm continue silently
- -i (—interactive): prompt user before deleting

  -r (—recursive): delete dir and its sub dirs

  -f (—force): ignore nonexistent files

  -v (—verbose)

tips: test rm with ls to see files are to be deleted

`ln`
- ln file link: create a hard link
- ln -s item link: create a symbolic link
- ln -s ../fun dir1/fun-sym: when create a symlink, we’re creating a text description of where the target file is relative to the symbolic link
- Hard link:
  - Cannot reference a file outside its own system (not on the same disk partition as the link)
  - May not reference a dir
- Symbolic link:
  - Overcome limitations of hard links
  - The pointed file and the corresponding symbolic link are largely indistinguishable: if write to link -> the file is written to. However when delete link, only the link is deleted
  - If the file is deleted first, the link points to nothing (broken). ls usually display broken links in a distinguishing color (ie. red)
- Files are made up of 2 parts:
  - The data part contains file’s content
  - The name part hold file’s name

A file always has at least one link because the file’s name is created by a link. Create hard links => actually create additional name part. The system assigns a chain of disk blocks to inode associated with the name part. Each hard link therefore refers to a specific inode containing the file’s content => 2 hard link is the same if have same inode (ls -li)

## Permissions

`id`

`chmod`

effective user ID, effective group ID, sticky bit

`umask`

`su` - switch user

`sudo` - can be configured to allow an ordinary user to execute commands as a different user (usually the superuser) in a controlled way (to see what privileges are granted by sudo, use `-l` option)

`chown` - change file owner and group. Superuser privileges are required to use this command.

`passwd`

## Working with Commands

`type`
- type command
- 4 types of commands:
  - an executable program: compiled binaries written C, C++; scripting languages such as Perl, Python, Ruby, etc.
  - a command built into the shell itself: like cd.
  - a shell function
  - an alias: user-define commands, built from other commands
  
`which`: display executable's location

`help`: get help for shell builtins
- help command, or
- command --help

`man`: display a program's manual page
- man uses less for displaying

`apropos`: search the list of man pages for possible matches based on a search term
- apropos search_term

`whatis`: display one-line manual page descriptions

`info`: GNU project provides an alternative to man pages for their programs.

`alias`
- no argument to list all aliases
- alias name='string'
- aliases vanish when shell session ends.

`unalias`: remove alias

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

## Seeing the World as the Shell Sees It

Expansion: when we press Enter, bash performs several substitution upon the text before it carries out the command.
- * expands to all file names in current dir.
- Tilde expansion: ~ expands to name of current directory of the named user (when used at begining of a word)
- Arithmetic expansion: `$((expression))`.
- Brace expansion: `{A, B, C}` to `A B C`, `{07..10}` to `07 08 09 10`, `{A..Z}`.
- Parameter expansion: `$USER`.
- Command substitution: `ls -l $(which cp)` or ls -l `which cp`.

Quoting: a mechanism called quoting to selectively suppress unwanted expansions. 
- Double quotes: if we place text inside double quote, all special characters used by the shell lose their special meaning and are treated and ordinary characters. Exception are $, \ and `.
- Single quotes: used to surpress ALL expansions.

Escaping Characters:
- `echo "\$5.00"`
- eliminate special meaning of a character ($, !, &, space, etc.) in a filename: `mv bad\&filename good_filename`
- escapse sequence: \a, \b, \n, \r, \t
- use echo with -e or `$' '` to enable interpretation of escapse sequences.

## Advanced Keyboard Tricks

`clear`

`history`
- !history_number: execute the command of the 88th line in the history list.
- Ctrl-r to search in the history incrementally. When found, enter to execute or Ctrl-j to copy it to the current command line.

History expansion:

|Key sequence|Desc|
|-|-|
|!! or up-enter|execute the last command|
|!number|explained|
|!string|repeat last history list item starting with string|
|!?string|repeat last history list item containing string|

Cursor movement:

|Key sequence|Desc|
|-|-|
|Ctrl-a|move cursor to begining of line|
|Ctrl-e|move cursor to end of line|
|Ctrl-f|move cursor forward 1 char|
|Ctrl-b|move cursor backward 1 char|
|Ctr-l|clear screen but keep the current command|
|Alt-right arrow|move cursor forward 1 word|
|Alt-left arrow|move cursor backward 1 word|

Modifying text:

|Key sequence|Desc|
|-|-|
|Ctrl-d|delete char at current cursor position|
|Ctrl-t|swap current char with prev char|

Cutting and Pasting text:

|Key sequence|Desc|
|-|-|
|Ctrl-k|Cut text from cursor location to end of line|
|Ctrl-u|Cut text from cursor location to begining of line|
|Ctrl-y|Paste text from the clipboard to the cursor location|

## Processes

background programs ~ daemon programs

`ps`: view processes
- ps x: all processes regardless of what terminal they are controlled by.
- STAT:
  - R: the process is running or ready to run.
  - S: sleeping, waiting for an event.
  - D: Uninterruptible sleep, waiting for I/O such as a disk drive.
  - T: Stopped (has been instructed to stop).
  - Z: Zombie process: the process that has terminated but has not been cleaned up by parent process.
  - <: high-priority process (given more time on the CPU for example)
  - N: low-priority process
- ps aux, column meaning:
  - USER: owner of the process.
  - %CPU: CPU usage in percent.
  - %MEM: Memory usage in percent.
  - VSZ: virtual memory size.
  - RSS: resident set size. Amount of physical memory the process is using in kb.
  - STARTED: Time when the process started.
  
`top`: view system processes in real time

Putting a process in background: `command &`, return `[job_number]PID`.

Putting a process in foreground: `fg %1`.

|Key sequence|Desc|
|-|-|
|Ctrl-C|Terminate a process|
|Ctrl-Z|Stop a process (and put it in background)|

`kill`
- `kill [-signal] PID`
- kill doesn't exactly kill processes, rather it sends them signals (like Ctrl-C sends INT signal, Ctrl-Z sends TSTP singal)
- Common signals by kill (`kill -l` for more detail):
  
  |Number|Name|Meaning|
  |-|-|-|
  |1|HUP|Hangup|
  |2|INT|Interrupt|
  |9|KILL|The process can't choose to handle/ignore this signal since the kernel immediately terminates the process, thus the process has no chance to clean up|
  |15|TERM|Default signal|
  |18|CONT||
  |19|STOP||
  |20|TSTP||
- You must be the owner of a process to send it signals with kill, otherwise you must have super privileges.
- Other common signals used by the system:
  
  |Number|Name|Meaning|
  |3|QUIT|Quit|
  |11|SEGV|Segmentation violation, sent if a program make illegal use of memory|
  |28|WINCH|Window change|
  

`jobs`: list the jobs that have been launched from our terminal.

`killall`: send signals to multiple processes.
- `killall [-u user] [-signal] name`

`sudo reboot`

`shutdown`
- sudo shutdown -h now: halt the system
- sudo shutdown -r now: reboot

## The Environment

The shell stores 2 basic types of data in the environment:
- shell variables: bits of data placed by bash.
- environment variables: everything else.

`printenv`: print environment variables
- no argument or `printenv VAR_NAME`

`set`: print both shell and environment variables

When we log on to the system, the bash program reads a series of configuration scripts called startup files. This is then followed by more startup files in our home directory that define our personal environment. Those startup files depend on the type of shell session being started:
- **A login shell session**: we are prompted for username and password (like whens start a virtual console session).

  Startups files for login shell session
  
  |File|Content|
  |-|-|
  |/etc/profile|A global configuration script that applies to all users|
  |~/.bash_profile|A user's personal startup file. This can be used to extend or override settings in the global configuration script|
  |~/.bash_login|If ~/.bash_profile is not found, bash attempts to read this script|
  |~/.profile|If neither ~/.bash_profile nor ~/.bash_login is found, bash attempts to read this file. This is the default in Debian-based distributions, such as Ubuntu|
  
- **A non-login shell session**: occurs when we launch a terminal session in the GUI.

  Startups files for non-login shell session
  
  |File|Content|
  |-|-|
  |/etc/bash.bashrc|A global configuration script that applies to all users|
  |~/.bashrc|A global configuration script that applies to all users. override settings in the global configuration script|
  
  Non-login shells also inherit the environment from their parent process, usually a login shell.
  
To add dirs to your PATH or define additional enviroment variables, place those changes in .bash_profile, place everything else in .bashrc
  
`export`:
- `export VAR` tells the shell to make the content of VAR available to child processes of this shell.


