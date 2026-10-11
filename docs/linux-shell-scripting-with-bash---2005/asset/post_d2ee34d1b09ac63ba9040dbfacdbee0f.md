
# Chapter 3 Files, Users, and Shell Customization

There are many switches for copy—the complete list is in the reference section at the end of this chapter. Some common switches are as follows:

- --force (-f) — Never prompts the user; always overwrites
- --interactive (-i) — Always prompts user
- -link (-1) — Creates a hard link instead of copying
- --parents (-p) — Appends the source path to destination directory
- --recursive (-R) — Copies any subdirectories
- --symbolic-link (-s) — Creates a symbolic link instead of copying
- --update (-u) — Overwrites old files or copies missing files

```
$ cp notes.txt old_notes.txt # copying
$ mkdir backup
$ cp old_notes.txt backup
$ ls backup
old_notes.txt
```

Like rm, some Linux distributions have --interactive on by default, warning when a file will be overwritten.

```
$ cp --interactive project_notes.txt old_notes
cp: overwrite `old_notes/project_notes.txt'? n
$
```

The mv (move) command moves and renames files. This is the same as making a copy of the file and deleting the original. Move also effectively renames a file by moving it to a new name in the same directory.

```
$ mv notes.txt project_notes.txt # renaming
```

The most common mv switches are similar to cp:

- --backup (-b) — Makes a backup of any existing file before overwriting by adding a - to the name
- --force (-f) — Never prompts the user; always overwrites
- --interactive (-i) — Always prompts the user before overwriting
- --update (-u) — Overwrites old files or copies missing files

There is no --recursive switch. When move moves a directory, it moves the directory and all its contents automatically.

The namei (name inode) command lists all the components in a path, including any symbolic links.

```
$ namei files
f: files
1 files -> /home/kem/bash/scripts
d /
d home
d kem
d bash
d scripts
```

In this case, the file named `files` is a symbolic link. Each of the files in the link path is a directory, marked with a d. Other file designations include l for symbolic link, s for socket, b for block device, c for character device, - for regular file, and ? for an error accessing a file in the path.

Complete file permissions, such as seen with `ls -l`, can be shown with the `-m (mode)` switch.

## Working with People

There are several commands for checking to see who is on the computer and what they are doing.

The `finger` command shows who is on the computer and provides additional information, including how long their session has been idle, and their contact information.

```
$ finger
Login    Name             TTY  Idle  When     Bldg.    Phone
dhu     Dick Hu         *tp6  4:25  Thu 14:12 4th Floor ext 2214
mchung  Michael Chung    *con  5:07  Fri 09:57 OS Support  ext 1101
bgill   Biringer Gill    *tp7   15   Fri 13:32
```

Some versions of Linux no longer include `finger` because of security concerns over `finger`'s `.plan` files. Read the `finger` manual page for more information.

There are several other commands with similar functions. The `users` command shows a list of login names.

```
$ users
bgill dhu mchung
```

The `who` command shows who is on the computer, which connection they are using, and when they signed on.

```
$ who
dhu     ttyp6      Mar 29 14:12
mchung  console     Apr  6 09:57
bgill   ttyp7       Apr  6 13:32
```

The `w` command provides even more information, including system statistics and what the users are currently running.

```
$ w
 3:18pm  up  9 days, 20:33,  3 users,  load average: 0.64, 0.66, 0.64
User     tty       login@        idle   JCPU   PCPU   what
dhu      ttyp6     2:12pm  4:28   8:01   8:01   csh
mchung   console    9:57am   5:10             sh
bgill    ttyp7      1:32pm   1.19           bash
```

## Shell Aliases

An alias is a short form of a command. The built-in `alias` command creates simple abbreviations for the current Bash session.

To create an alias, use the `alias` command to assign a command and its switches a name.

```
$ alias lf='ls -qPl'
$ lf
-rw-r----- 1 kurtch devgroup 10809 Apr 6 11:00 assets.txt
-rw-r----- 1 kurtch devgroup 4713 Mar 9 2000 mailing_list.txt
```

Typing the alias command by itself, or with the `-p` switch, lists the current aliases.

```
$ alias
alias lf='ls -qPl'
```

Bash interprets an alias only once, allowing the aliasing of a command with its own name.

```
$ alias ls='ls -qP' # Bash isn't confused
```

Normally, only the first word of a command is checked for an alias. As a special exception, if the last character in the alias string is a blank, Bash checks the next word in the command to see whether it is also an alias.

There is no method for giving arguments to an alias. If arguments are needed, define a more powerful shell function instead.

The built-in `unalias` command removes an alias. Use the `-a` switch to remove them all.

Most Linux distributions have aliases defined for common commands. `dir`, for example, is often an alias for `ls`. Some distributions define an alias for commands such as `rm -i` to force user prompting, which is not required by default. This can be a problem for some users such as experienced Unix programmers who are used to working with these features disabled. Use `unalias` to remove any aliases that you don't want to use.

Aliases mixed with shell functions can be confusing because aliases are expanded only when a line from a script is read. If aliases are used in a shell function, they are expanded when the shell function is defined, not when it is executed. For this reason, it is safer to avoid aliases altogether in shell scripts. However, they can be turned on in scripts using the `shopt -s expand_aliases` command.

## The Bash Hash Table

When a command is executed without naming a path, the shell searches for the command (in the directories listed in the `PATH` variable). When the Bash finds the command, it remembers where it is, storing the location in a *hash table*. Thereafter, Bash checks the table for the location of the command instead of searching for the command again, making commands run faster. However, if the command moves after Bash has recorded its location, the shell won't be able to find the command.

The built-in `hash` command maintains the hash table. Without any switches, `hash` lists the memorized commands, where they are, and the number of times the command has been executed during this session.

```
$ hash
hits      command
  1       /bin/ls
  1       /bin/uname
  1       /usr/bin/tput
  1       /bin/stty
  1       /usr/bin/uptime
  1       /usr/bin/man
```

When a command is specified, Bash searches for the new location of the command. For example, if you create your own `ls` command in your current directory, and the `PATH` variable gives precedence to files in your current directory, the `hash ls` command finds your `ls` command first, replacing `/bin/ls` with `./ls`.

```
$ hash ls
$ hash
hits      command
  1       /bin/touch
  0       ./ls
  1       /bin/cmdop
```

The `-p` (`path`) switch explicitly sets a path for a command. The `-d` (`delete`) switch deletes a specific entry, and `-r` (`remove`) clears the hash table, removing all commands. The `-t` (`table`) option lists the pathnames for specific commands, and `-l` (`list`) lists the commands in a format that allows them to be reused by the `hash` command.

```
$ hash -t ls less
ls        /bin/ls
less      /usr/bin/less
```

## Customizing Your Prompt

The default Bash interactive prompt is a dollar sign ($), although some distributions use a different symbol. Most Linux distributions redefine the prompt to include additional information, such as your current login and computer, which is useful when you're moving between accounts and computers.

If a variable named `PS1` (`prompt string 1`) is defined, Bash will use the value of this variable for your main prompt. If you include variable names in the string, Bash will substitute the value of the variables into your prompt.

```
$ declare -x PS1="Bash $ "
Bash $ pwd
/home/ke/kbrutch/archive
Bash $
```
