
| `set -o vi` | Enable command completion with vi commands in the ksh shell. |
| `sh` | Start a sh (Bourne) subshell or run a sh shell script. |
| `stty erase '^?'` | Make Delete erase characters to the left of the cursor. |
| `stty erase '^H'` | Make Ctrl H erase characters to the left of the cursor. Type `stty erase` then press Ctrl V Ctrl H. |
| `su - yourid` | Start a new log-in shell as yourid. |
| `su user` | Switch user to user. |
| `tcsh` | Start a tcsh subshell or run a tcsh shell script. |
| `zsh` | Start a zsh subshell or run a zsh shell script. |

## Table A.4

### Creating and Editing Files

| COMMAND | DESCRIPTION |
|---|---|
| `ed` | Choose a line-oriented text editor. |
| `emacs` | Choose a tremendously powerful, somewhat easy to use text editor. |
| `emacs -n` | Open emacs and force a terminal-window- (not graphical window-) oriented session. |
| `emacs filename` | Open emacs and edit filename. |
| `joe` | Choose a fairly friendly editor. |
| `pico` | Choose for menu-oriented, user-friendly text editing. |
| `pico filename` | Open and edit filename in pico. |
| `pico -w filename` | Disable word wrapping for filename in pico. This is particularly useful for configuration files. |
| `vi` | Choose a powerful editor with lots of power but little ease of use. |
| `vi filename` | Open and edit filename in vi. |

## Table A.5

### Controlling File Ownership and Permissions

| COMMAND | DESCRIPTION |
|---|---|
| `chgrp` | Change the group association of files or directories. |
| `chgrp groupname filename` | Change the group association of filename to groupname. |
| `chgrp -R group directory` | Recursively change the group association of directory and all subdirectories and files within it to group. |
| `chmod` | Change the permissions for a file or directory. |
| `chmod a-w file` | Remove write permission for file for all (everyone). |
| `chmod g+w file` | Add write permission for file for the current group. |
| `chmod -R go-rwx *` | Revoke all permissions from everyone except the user for all files in the current directory and all subdirectories and their contents. |
| `chmod u=rwx,g=rx,o=r file` | Set the permissions on file to user read, write, and execute, group read and write, and others read. |
| `chmod ugo- *` | Revoke all permissions for everything in the current directory from everyone. |
| `chown` | Change the ownership of files or directories. |
| `chown -R user directory` | Recursively change the ownership of Directory and all contents to user. |
| `chown user file` | Change the ownership of file to user. |
| `umask 022` | Specify the default permissions for all created files. |

## Table A.6

### Manipulating Files

| Command | Description |
|---|---|
| `awk` | Manipulate a file as a database. |
| `awk '/CA/{ print $2 $1 $7 }' file` | Select (and display) three fields in each record in file on lines that contain "CA". |
| `awk '{ print $1 }' file` | Select (and display) the first field in each record in file. |
| `awk -f script.awk file` | Run an awk command from a script called script.awk on file. |
| `awk -F, '{ print $1 }' file > newfile` | Select the first field in each record in file, specifying that a "," separates fields, and redirect the output to newfile. |
| `awk -F: '{ print $2 " " $1 " in " $7 }' file` | Select (and display) several fields and some text for each record in file, using a colon (:) as a field delimiter. |
| `basename` | Remove the path from a filename, leaving only the name proper. Good to use in scripts to display just a filename. |
| `cmp newfile oldfile` | Compare newfile to oldfile. |
| `crypt` | Encrypt or decrypt a password-protected file. |
| `csplit` | Divide files based on line number or other characteristics. |
| `diff -b newfile oldfile` | Find differences (ignoring white space) between newfile and oldfile. |
| `diff Directory Newdirectory` | Find differences between Directory and Newdirectory. |
| `diff -i newfile oldfile` | Find differences (except in case) between newfile and oldfile. |
