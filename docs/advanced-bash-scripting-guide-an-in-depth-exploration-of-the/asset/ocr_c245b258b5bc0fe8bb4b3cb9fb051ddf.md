# Advanced Bash-Scripting Guide

The familiar cd change directory command finds in scripts where execution of a command requires being in a specified directory.

```
cd /source/directory tar cf - . | (cd /dest/directory tar xpvf -)
from the previously cited example by Alan Cox
```

- The P (physical) option to cd causes it to ignore symbolic links.

cd - changes to $PWD, the previous working directory.

The cd command does not function as expected when presented with two forward slashes.

```
bash$ cd //
bash$ pwd
```

The output should, of course, be /. This is a problem both from the command-line and in a script.

pwd

Print Working Directory. This cd gives the user (or script's) current directory (see Example 15-9). The effect is ideal to reading the value of the builtin variable $PWD.

pushd, popd, dirs
This command is a mechanism for bookmarking working directories, a means of moving back and forth through directories in an orderly manner. A pushdown stack is used to keep track of directory names. Options allow various manipulations of the directory stack.

> pushd dir-name pushes the dir-name onto the directory stack (to the top of the stack) and simultaneously changes the current working directory to dir-name

popd removes (pops) the top directory path name off the directory stack and simultaneously changes the current working directory to the directory now at the top of the stack.

dirs lists the contents of the directory stack (compare this with the $DIRSTACK variable). A successful pushd or popd will automatically invoke dirs.

Scripts that require various changes to the current working directory without hard-coding the directory name can make good use of these commands. Note that the implicit $DIRSTACK array, accessible within a script, holds the contents of the directory stack.

# Example 15-9. Changing the current working directory

```
#!/bin/bash
dir1=/usr/local
dir2=/var/spool

push $dirs (list directory stack to stdout).
# Will do an automatic "Now in directory `pwd`." # Uses back-quoted 'pwd'.
```

Chapter 15. Internal Commands and Builtins

192