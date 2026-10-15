```
set size = $fileinfo[5]
echo "Name      Inode      Size"
echo
echo "$filename    $inode    $size"
exit 0
endif
echo "$0: argument must be an ordinary file"
exit 1
```

Python code

```
#!/usr/local/bin/python
import os
import sys
if len(sys.argv) == 1 or len(sys.argv) > 2:  #check for no or too many arg(s)
    print "Usage: ", sys.argv[0], "is not an ordinary file"
    sys.exit(1)
if sys.argv[1].startswith('.'):      #added check for dot files
    print "Usage: ", sys.argv[1], "is a dot file"
    sys.exit(1)
if os.path.isfile(sys.argv[1]):      #bingo, get stats
    filename = sys.argv[1]
    fileinfo = os.stat(filename)
    print "Filename  inode   size"
    Print " "
    print filename, fileinfo.st_ino, fileinfo.st_size
    sys.exit(0)
else:                               # argument must be a directory
    print sys.argv[1], " argument must be an ordinary file"
    sys.exit(1)
```

# 16.4.2 Basic User File Maintenance

A very useful and important aspect of your interaction with a computer is how effectively you can maintain the files on your system. The Python standard library, and many user-written libraries and modules, can help you do this efficiently in UNIX. You can utilize the extensive syntax and multiparadigm programming capabilities of Python to go far beyond the capabilities of doing operating system and file maintenance available in any of the UNIX shell programs. This section assumes that you have already read and done the exercises and problems in Chapters 4 through 9 that deal with file manipulation. User file maintenance consists of creating, saving, organizing, and deleting files on your system, in your own account. Chapter 23 describes and details how the same things can be done on a system-wide level by the person that