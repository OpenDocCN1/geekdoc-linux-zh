# 32. Using regular expression-based search

The ‘re’ module makes it very easy to use regexp-based searches. You can use the function re.search() with a regexp-based expression.

```
Check out the example below.

Example:
>>> import re
>>> s = “Kunal is a bad boy”
>>> if re.search(“K”, s): print “Match!”
Match!
>>> if re.search(“[^a-z]”, s): print “Match!” # char literal
... 
Match!
>>> if re.search(“[0-9]”, s): print “Match!” # digits class
...
```

# 33. Working with bz2 (.bz2) compression format

You can use the module ‘bz2’ to read and write data using the bz2 compression algorithm.

```
bz2.compress() : For bz2 compression
bz2.decompress() : For bz2 decompression

Example:
# File: bz2-example.py
import bz2
MESSAGE = “Kunal is a bad boy”
compressed_message = bz2.compress(MESSAGE)
print “original:”, repr(MESSAGE)
print “compressed message:”, repr(compressed_message)
print “decompressed message:”, repr(bz2.decompress(compressed_message))

Output:
$ python bz2-example.py
original: ‘Kunal is a bad boy’
compressed message: ‘BZh91AY&SY...’
decompressed message: ‘Kunal is a bad boy’
```

# 34. Using SQLite database with Python

SQLite is fast becoming a very popular embedded database because of its zero configuration needed, and superior levels of performance. You can use the module ‘sqlite3’ in order to work with SQLite databases.

```
Example:
>>> import sqlite3
>>> connection = sqlite3.connect(‘test.db’)
>>> curs = connection.cursor()
>>> curs.execute(‘’’create table item (id integer primary key, item text unique, name text, item_code text, price real)’’’)
<sqlite3.Cursor object at 0x1004a2b30>
```

# 35. Working with zip files

You can use the module ‘zipfile’ to work with zip files.

```
zipfile.ZipFile(filename, mode[‘r’, compression[, allowZip64=True]])
Open a zip file, where the file can be either a path to a file (a string) or a file-like object.
zipfile.close()
Close the archive file. You must call ‘close()’ before exiting your program or essential records will not be written.
zipfile.extract(member[, path[, pwd]])
```

Extract a member from the archive to the current working directory. ‘member’ must be its full name (or a zipinfo object). Its file information is extracted as accurately as possible. ‘path’ specifies a different directory to extract to. ‘member’ can be a filename or a zipinfo object.

# 36. Using UNIX-style wildcards to search for filenames

You can use the module ‘glob’ to find all the pathnames matching a pattern according to the rules used by the UNIX shell. *, ?, and character ranges expressed with [] will be matched.

```
Example:
>>> import glob
>>> glob.glob(‘./[0-9].*’)
[‘./1.gif’, ‘./2.txt’]
>>> glob.glob(‘*.gif’)
[‘1.gif’, ‘card.gif’]
>>> glob.glob(‘?.gif’)
[‘1.gif’]
```

# 37. Performing basic file operations (copy, delete and rename)

You can use the module ‘shutil’ to perform basic file operation at a high level. This module works with your regular files and so will not work with special files like named pipes, block devices, and so on.

```
shutil.copy(src,dst)
Copies the file src to the file or directory dst.
shutil.copymode(src,dst)
Copies the file permissions from src to dst.
shutil.move(src,dst)
Moves a file or directory to dst.
shutil.copytree(src, dst, symlinks=[, ignore])
Recursively copy an entire directory src.
shutil.rmtree(path [, ignore_errors [, onerror]])
Deletes an entire directory.
```

# 38. Executing UNIX commands from Python

You can use double commands to execute UNIX commands. This is not available in Python 3 – instead you need to use the module ‘subprocess’.

```
Example:
>>> import commands
>>> commands.getoutput(‘ls’)
‘bz2-example.py\ntest.py’
```

# 39. Reading environment variables

You can use the module ‘os’ to gather operating-system-specific information.

```
Example:
>>> import os
>>> os.path <module ‘posixpath’ from ‘/usr/lib/python2.6/posixpath.pyc’>
>>> os.environ {‘LANG’: ‘en_US’, ‘TERM’: ‘xterm-color’, ‘SHELL’: ‘/bin/bash’, ‘LESSCLOSE’: ‘/usr/bin/lesspipe %s %s’, ‘XDG_SESSION_COOKIE’: ‘4925c4644597c791c704656354adf56d6-1257673132.347986-1117793225’, ‘SHLVL’: ‘1’, ‘SSH_TTY’: ‘/dev/pts/2’, ‘PWD’: ‘/home/kunal’, ‘LESSOPEN’: ‘| /usr/bin/lesspipe’}
>>> os.name
‘posix’
>>> os.linesep
‘\n’
```