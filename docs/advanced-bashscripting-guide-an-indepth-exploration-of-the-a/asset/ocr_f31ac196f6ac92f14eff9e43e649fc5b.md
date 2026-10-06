# Advanced Bash–Scripting Guide

| | | | | |
|---|---|---|---||
| -rw--r--r-- | 1 bozo bozo | 4034 Jul 18 22:04 datal.xrolo |
| -rw--r--r-- | 1 bozo bozo | 4602 May 25 13:58 datal.xrolo.bak |
| -rw--r--r-- | 1 bozo bozo | 877 Dec 17 2000 employment.xrolo |

shred
ly erase by overwriting it multiple times with random bit patterns before deleting. This command has the same effect as Example 12–36, but does it in a more thorough and elegant manner.

This is one of the GNU fileutils.

Using shred on a file may not prevent recovery of some or all of its contents using forensic technology.

locate, slocate
The locate command searches for files using a database stored for that purpose. The locate command is the secure version of locate (which may be aliased to slocate).

# $bash locate hickson

```
/usr/lib/xhem/catalogs/hickson.edb
```

strings
 the strings command to find printable strings in a binary or data file. It will list sequences of printable characters found in the target file. This might be handy for a quick ‘n dirty examination of a core dump for looking at an unknown graphic image (strings image–file |) more might show something like JFIE, which would identify the file as a jpeg graphic). In a script, you would probably parse the output of strings grep or sed. See Example 10–7 and Example 10–9.

Example 12–26. An "improved" strings command

```
#!/bin/bash
# wstrings.sh: "word-strings" (enhanced "strings" command)
#
# This script filters the output of "strings" by checking it
# against a standard word list file.
# This effectively eliminates all the gibberish and noise,
# and outputs only recognized words.

######################################################################
# Standard Check for Script Argument(s)
ARGS=1
_BADARGS=65
_NOFILE=66

if [ $# -ne $ARGS ]; then
then
echo "Usage: `basename $0` filename"
```

# 12.5. File and Archiving Commands

*