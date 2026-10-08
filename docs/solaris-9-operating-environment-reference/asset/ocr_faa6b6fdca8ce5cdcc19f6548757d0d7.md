# 1530

# view

# Synopsis

# See Also

ctags(1), ed(1), edit(1), ex(1), intro(1), attributes(5), environ(5),
largefile(5), standards(5)
Solaris Advanced User's Guide

# Author

vi and ex were developed by The University of California, Berkeley, California,
Computer Science Division, Department of Electrical Engineering and Computer
Science.

# view — Screen-Oriented Visual Display Editor Based on ex

```
/usr/bin/view [- -s] [-L] [-R [filename] [-S] [-t tag] [-v]
[-V] [-x] [-wn] [-C]
/usr/xpg4/bin/view [- -s] [-1] [-L] [-R [filename] [-t tag]
[-V] [-x] [-wn] [-C] [+command |c command] filename...
/usr/bin/view [- -s] [-1] [-L] [-R [filename] [-t tag] [-v]
[-x] [-wn] [-C] [+command |c command] filename...
/usr/xpg4/bin/view [- -s] [-1] [-L] [-R [filename] [-t tag] [-v]
[-V] [-x] [-wn] [-C] [+command |c command] filename.
```

# Description

See vi(1).

# vipw — Edit the Password File

# Synopsis

```
/usr/ucb/vipw
```

# Description

vipw edits the password file while setting the appropriate locks and does any necessary
processing after the password file is unlocked. If the password file is already being
edited, you are told to try again later. The vi(1) editor is used unless the environment
variable VISUAL or EDITOR indicates an alternative editor.
vip performs a number of consistency checks on the password entry for root
do not allow a password file with a “mangled” root entry to be installed. It also checks
t /etc/shells file to verify the login shell for root.

# Files

```
/etc/passwd
/etc/shells *
```