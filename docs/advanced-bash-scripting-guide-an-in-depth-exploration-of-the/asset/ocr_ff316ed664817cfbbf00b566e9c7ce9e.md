# Advanced Bash-Scripting Guide

redirection/from/to stdin or stdout [dash].

```
bash$ cat -
abc
abc
...
```

Ctl-D
As expected, cat echoes stdin, in this case keyboarded user input, to stdout. But does I/O redirection using have real-world applications?

```
(cd /source/directory && tar cf - . | (cd /dest/directory && tar xpvf -)
# Move entire file from one directory to another
# [course Alex Cox <a.cox@wansea.ac.uk>, with a minor change
# 1) cd /source/directory
# Source directory, where the files to be moved.
# 2) &&
# "And-list": if the 'cd' operation successful,
# then execute the next command.
# 3) tar cf -
# The 'c' option 'tar' archiving command creates a new archive,
# the 'f' (file) option, followed by '-' designates the target tree
# as stdout, and do it in its current directory ('.').
# 4) |
# Piped to
# (...)
# 5)
# a subshell
# 6) cd /dest/directory
# Change to the destination directory.
# 7) &&
# "And-list", as above
# 8) tar xpvf
# Unarchive ('x'), preserve ownership and file permissions ('p'),
# and send verbose messages to stdout ('v'),
# reading data from stdin followed by '-'.
# Note that 'x' is a command, and 'p', 'v', 'f' are options.
# Whew!
```

```
# More elegant than, but equivalent to:
# cd /source/directory
# tar cf - | (../dest/directory; tar xpvf -)
# Also having same effect:
# cp -a /source/* /dest/directory
# Or:
# cp -a /source/* /source/directory/.[*] /dest/directory
# If there are hidden files in /source/directory.
bunzip2 -c linux-2.6.16.tar.bz2 | tar xvf
# --uncompress tar file---| --then pass it to "tar"
# If "tar" has not been patched to handle "bunzip2"
## this needs to be done in two discrete steps, using a pipe.
# The purpose of the exercise is to unarchive bzipped kernel source.
```

Chapter 3. Special Characters