# Part II Shell Scripting Basics

```
exec 3>$tempfile

echo "This script writes to temp file $tempfile"

echo "This is the first line" >&3
echo "This is the second line." >&3
echo "This is the last line." >&3
exec 3&-

echo "Done creating temp file. The contents are:"
cat $tempfile
rm -f $tempfile 2> /dev/null
./test19
This script writes to temp file test19.vCHoya
Done creating temp file. The contents are:
This is the first line
This is the second line.
This is the last line.
$ -al test19*
-rwxr-xr-r--      1 rich      rich      356 Oct 29 22:03 test19* 
```

The script uses the mkdir command to create a temporary file and assigns the file name to $tempfile variable. It then uses the file as the output redirection file for file descriptor 3. After displaying the temporary file name on STDOUT, it writes a few lines to the temporary file, then it closes the file descriptor. Finally, it displays the contents of the temporary file and uses the rm command to remove it.

# Creating a temporary file in /tmp

The -t option forces mkdir to create the file in the temporary directory of the system. When you use this feature, the mkdir command returns the full pathname used to create the temporary file, not just the filename:

```
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
$ -al /tmp/test*
-rw-r--      1 rich 0 2007-10-29 18:41 /tmp/test.xG3374 
```

The mkdir command returns the full pathname, which you can then reference from any directory on the Linux system, no matter where it places the temporary directory:

```
$ cat test20
!/bin/bash
# creating a temp file in /tmp
```

```
tempfile=`mkdir -t tmp.XXXXXX`
```