# # Python essentials

# ## **32** Using regular expression-based search

You can use the function 're.search()' with a regexp-based expression. Check out the example below.

```
**Example:**
>>> import re
>>> s = "Kunal is a bad boy"
>>> if re.search("K", s): print "Match!" # char literal

...
Match!
>>> if re.search(["A-Z"], s): print "Match!" # char class
... # match either at-sign or capital letter
Match!
>>> if re.search("4d", s): print "Match!" # digits class
...
```

# ## **33** Working with bzip2 (.bz2) compression format

You can use the module 'bz2' to read and write data using the bzip2 compression algorithm.
bz2.compress():  For bz2 compression
bz2.decompress(): For bz2 decompression

```
**Example:**
# File: bz2-example.py
import bz2
MESSAGE = "Kunal is a bad boy"
compressed_message = bz2.compress(MESSAGE)
decompressed_message = bz2.decompress(compressed_message)
print "original:", repr(MESSAGE)
print "compressed message:", repr(compressed_message)
print "decompressed message:", repr(decompressed_message)

**Output:**
[~/src/python $:] python bz2-example.py
original: 'Kunal is a bad boy'
compressed message: 'Bzh1A\x83Y\xc4\x6f\x9b\x00\x00\x02\x15\x00e\x00\n\x80\x84\x8a \x00\n\x00\x0c\x84\r\n\x83\c\x2\x0\x8\xdf\x5\x9b\x19\x80\n\xf8\x00\xd9\xc2\xc2\xd4\x86\x0\x86 z\xc\xe0\'
decompressed message: 'Kunal is a bad boy'
```

# ## **34** Using SQLite database with Python

SQLite is fast becoming a very popular embedded database because of its zero configuration needed, and superior levels of performance. You can use the module 'sqlite3' in order to work with SQLite databases.

```
**Example:**
>>> import sqlite3
>>> connection = sqlite.connect("test.db")
>>> curs = connection.cursor()
>>> curs.execute("""create table item
... (id integer primary key, itemno
... text unique,
... scandesc text, descr text, price
... real)""")
<sqlite3.Cursor object at 0x1004a2b30>
```

# ## **35** Working with zip files

You can use the module 'zipfile' to work with zip files.

```
zipfile.ZipFile(filename [, mode [, compression [.,allowZip64]]])
Open a zip file, where the file can be either a path to a file (a string) or a file-like object.
zipfile.close()
Close the archive file. You must call 'close()' before exiting your program or essential records will not be written.
zipfile.extract(member [, path [, pwd]]])
Extract a member from the archive to the current working directory. 'member' must be its full name (or a zinfo object). 'path' specifies a different directory to extract to. 'member' can be a filename or a zinfo object. 'pwd' is the password used for encrypted files.
```

# ## **36** Using UNIX-style wildcards to search for filenames

You can use the module 'glob' to find all the pathnames matching a pattern according to the rules used by the UNIX shell. '*', '?', and character ranges expressed with [] will be matched.

```
**Example:**
>>> import glob
>>> glob.glob('[/.0-9]_*.*)'
['/1.gif', '/2.txt']
>>> glob.glob(*.gif')
['1.gif', 'card.gif']
>>> glob.glob('?.gif')
['1.gif']
```

# ## **37** Performing basic file operations (copy, delete and rename)

You can use the module 'shutil' to perform basic file operation at a high level. This module works with your regular files and so will not work with special files like named pipes, block devices, and so on.

```
shutil.copy(src, dst)
Copies the file src to the file or directory dst.
shutil.copyfile(src, dst)
Copies the file permissions from src to dst.
shutil.move(src, dst)
Moves a file or directory to dst.
shutil.copytree(src, dst, symlinks [, ignore[]])
Recursively copy an entire directory at src.
shutil.rmtree(path [, ignore_errors [, onerror]]
Deletes an entire directory.
```

# ## **38** Executing UNIX commands from Python

This is not available in Python 3 - instead you need to use the module 'subprocess'.

```
**Example:**
>>> import commands
>>> commands.getoutput('ls')
'bz2-example.py\ntest.py'
```

# ## **39** Reading environment variables

You can use the module 'os' to gather operating-system-specific information:

```
**Example:**
>>> import os
>>> os.path.module 'posixpath'
>>> print '/usr/lib/python2.6/posixpath'
#  'en_US\n' "X_term-color" "SHELL:" /bin/bash' "LESSCLOSE:' /usr/bin/lesspipe "Xs" "XDG_SESSION_COOKIE:' '925c4644957c791c784656354ad\x568-1257673132.347986.1177197325' "SHLVL:" 1, "SSH_TTY:" /dev/pts/2, "PWD" " /home/kunal", "LESSOPEN" " /usr/bin'
lesstpipe
... }
>>> os.name
'posix'
>>> os.linesep
'\n'
```