# Advanced Bash–Scripting Guide

Strips the path information from a file name, printing only the name. The construction basename $0 lets the script its name, that is, the name it invoked. This can be used for "usage" messages if, for example a script is called with missing arguments:

```
echo "Usage: basename $0 arg1 arg2 ... argn"
dirname
```

Strips the basename from a filename, printing only the path information.

basename and dirname can operate on any arbitrary string. The argument does not need to refer to an existing file, or even a filename for that matter (Example A–7).

# Example 12–27. basename and dirname

```
#!/bin/bash
a=/home/bozo/daily-journal.txt
echo "Basename of /home/bozo/daily-journal.txt = \basename $a\"
echo "Dirname of /home/bozo/daily-journal.txt = \dirname $a\"
echo "My own home is \basename ~/" # Also works with just .
echo "The home of my home is \dirname ~/" # Also works with just .
exit 0
```

Utility for splitting a file into smaller chunks. Usually used for splitting large files in order to back them up on floppies or preparatory to e-mailing or uploading them.

# sum, cksum, md5sum

These are utilities for generating checksums. A cksum is a number mathematically calculated from the contents of a file, for the purpose of checking its integrity. A script might refer to a list of checksums for security purposes, such as checking the contents of key system files have not been altered or corrupted. The md5 command is the most appropriate of these security applications.

Note that cksum also shows the size, in bytes, of the target file.

```
bash cksum /boot/mlinuz
1670054224 804083 /boot/mlinuz

bash md5sum /boot/mlinuz
0f43eceea8f09e0a2b5c1cdf333ba /boot/mlinuz
```

# Encoding and Encryption

uuencode

# 12.5. File and Archiving Commands