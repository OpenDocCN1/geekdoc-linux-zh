# Advanced Bash-Scripting Guide

```
# Bash version info:
for n in 0 1 2 3 4 5
do
  echo "BASH_INFO[$n] = $${BASH_INFO[$n]}"
done
```

```
# BASH_INFO[0] = 3 # Major version no.
# BASH_INFO[1] = 00 # Minor version no.
# BASH_INFO[2] = 14 # Patch level.
# BASH_INFO[3] = 1 # Build version.
# BASH_INFO[4] = release # Release status.
# BASH_INFO[5] = 1386-redhat-linux-gnu # Architecture
# (same as $MACHYPE)
```

$BASH_VERSION

The version of bash installed on the system

```
bash$ echo $BASH_VERSION
3.2.25(1)-release
```

```
tcsh$ echo $BASH_VERSION
BASH_VERSION: Undefined variable.
```

Checking $BASH_VERSION is a good method of determining which shell is running. SHELL does not necessarily give the correct answer.

$CDPATH
A colon-separated list of search paths available to the cd command, similar in function to the PATH variable for binaries. $CDPATH variable may be set in the local ~/.bashrc file.

```
bash$ cd bash-doc
bash: bash-doc: No such file or directory
```

```
bash$ CDPATH=/usr/share/doc
bash$ cd bash-doc
/usr/share/doc/bash-doc
```

```
bash$ echo $PWD
/usr/share/doc/bash-doc
```

$DIRSTACK
The value in the directory stack [41] (affected by pushd and popd).

This builtin variable corresponds to the dirs command, however dirs shows the entire contents of the directory stack.

$EDITOR
The default editor invoked by a script, usually vi or emacs.

$UID
"effective" user ID number

Identification number of identity the current user has assumed, perhaps by means of su. The UID is not necessarily the same as the SUID.

Chapter 9. Another Look at Variables