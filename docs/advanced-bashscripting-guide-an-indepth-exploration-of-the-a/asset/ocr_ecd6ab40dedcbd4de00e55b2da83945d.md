# Advanced Bash–Scripting Guide

$bash whichis rm

```
/usr/bin/rm
```

whereis

Similar to whichis, above, whereis command-xxx gives the full path to "command-xxx", but also to its manpage.

$bash whereis rm

```
rm: /bin/rm /usr/share/man/man1/rm.1.bz2
```

whatis

whatis filexxx looks up "filexxx" in the whatis database. This is useful for identifying system commands and important configuration files. Consider it a simplified man command.

$bash whatis whatis

```
whatis (1) search the whatis database for complete words
```

Example 12–25. Exploring /usr/X11R6/bin

```
#!/bin/bash

# What are those mysterious binaries in /usr/X11R6/bin?
DIRECTORY="/usr/X11R6/bin"
# Try also "/bin", "/usr", "/local/bin", etc.

for file in $DIRECTORY
do
    whatis basename '$file' # Echoes info about the binary.
done

exit 0
# You may wish to redirect output of whatis, like so:
#whatis.sh >>whatis.db
# or view it a page at a time on stdout,
#whatis.sh | less
```

See also Example 10–3.

vdir

Show a detailed directory listing. The effect is similar to ls -l.

This is one of the GNU fileutils.

bash$ vdir
total 10
-rw-r--r 1 bozo bozo 4034 Jul 18 22:04 datal.xrolo
-rw-r--r 1 bozo bozo 4602 May 25 13:58 datal.xrolo.bak
-rw-r--r 1 bozo bozo 877 Dec 17 2000 employment.xrolo

# 12.5. File and Archiving Commands