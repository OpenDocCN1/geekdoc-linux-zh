
# Suppressing Command Output

There are times when you don't want to display any output from your script. This often occurs if you're running a script as a background process (see Chapter 13). If any error messages occur from the script while it's running in background, the shell e-mails to the owner of the process. This can get tedious, especially if you run scripts that generate minor nuisance errors.

To solve that problem, you can redirect STDERR to a special file called the null file. The null file is pretty much what it says it is, a file that contains nothing. Any data that the shell outputs to the null file is not saved, thus lost.

The standard location for the null file on Linux systems is /dev/null. Any data you redirect to that location is thrown away and doesn't appear:

```
$ ls -al > /dev/null
$ cat /dev/null
$
```

This is a common way to suppress any error messages without actually saving them:

```
$ ls -al badfile test16 2> /dev/null
-rw-xr-r-- 1 rich      rich      135 Oct 29 19:57 test16*
$
```

You can also use the /dev/null file for input redirection as an input file. Since the /dev/null file contains nothing, it is often used by programmers to quickly remove data from an existing file without having to remove the file and recreate it:

```
$ cat testfile
This is the first line.
This is the second line.
This is the third line.
$ cat /dev/null > testfile
$
```

The file testfile still exists on the system, but now it is empty. This is a common method to clear out log files that must remain in place for applications to operate.

# Using Temporary Files

The Linux system contains a special directory location for temporary files. Linux uses the /tmp directory for files that don't need to be kept indefinitely. Most Linux distributions configure the system to automatically remove any files in the /tmp directory at bootup.

# Presenting Data 12

Any user account on the system has privileges to read and write files in the /tmp directory. This feature provides an easy way for you to create temporary files that don't necessarily have to worry about cleaning up.

There's even specific command to use for creating a temporary file. the mktemp command allows you to easily create a unique temporary file in the /tmp folder. The shell creates the file but doesn't use your default umask value (see Chapter 6). Instead, it only assigns read and write permissions to the file's owner and makes you the owner of the file. Once you create the file, you have full access to read and write to and from it from your script, but no one else will be able to access it (other than the root user of course).

# Creating a local temporary file

By default, mktemp creates a file in the local directory. To create a temporary file in a local directory with the mktemp command, all you need to do is specify a filename template. The template consists of any text filename, fix six X's appended to the end of the filename:

```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------r 1 rich 0 Oct 29 21:30 testing.Ufii3
$
```

The mktemp command replaces the six X's with a six-character code to ensure the filename is unique in the directory. You can create multiple temporary files and be assured that each one is unique:

```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.1VBtkw
$ mktemp testing.XXXXXX
testing.PqgKG
$ ls -l testing*
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1DRLuV
-rw------- 1 rich rich 0 Oct 29 21:57 testing.PggKNG
-rw------- 1 rich rich 0 Oct 29 21:30 testing.Ufii3
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1VBtkw
$
```

As you can see, the output of the mktemp command is the name of the file that it creates. When you use the mktemp command in a script, you'll want to save that filename in a variable, so you can refer to it later in the script:

```
$ cat test19
#!/bin/bash
# creating and using a temp file
tempfile=`mktemp test19.XXXXXX`
```

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
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
```

# Presenting Data

Any user account on the system has privileges to read and write files in the /tmp directory. This feature provides an easy way for you to create temporary files that don't necessarily have to worry about cleaning up.

There's even specific command to use for creating a temporary file. the mktemp command allows you to easily create a unique temporary file in the /tmp folder. The shell creates the file but doesn't use your default umask value (see Chapter 6). Instead, it only assigns read and write permissions to the file's owner and makes you the owner of the file. Once you create the file, you have full access to read and write to and from it from your script, but no one else will be able to access it (other than the root user of course).

# Creating a local temporary file

By default, mktemp creates a file in the local directory. To create a temporary file in a local directory with the mktemp command, all you need to do is specify a filename template. The template consists of any text filename, fix six X's appended to the end of the filename:

```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------r 1 rich 0 Oct 29 21:30 testing.Ufii3
$
```

The mktemp command replaces the six X's with a six-character code to ensure the filename is unique in the directory. You can create multiple temporary files and be assured that each one is unique:

```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.1VBtkw
$ mktemp testing.XXXXXX
testing.PqgKG
$ ls -l testing*
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1DRLuV
-rw------- 1 rich rich 0 Oct 29 21:57 testing.PggKNG
-rw------- 1 rich rich 0 Oct 29 21:30 testing.Ufii3
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1VBtkw
$
```

As you can see, the output of the mktemp command is the name of the file that it creates. When you use the mktemp command in a script, you'll want to save that filename in a variable, so you can refer to it later in the script:

```
$ cat test19
#!/bin/bash
# creating and using a temp file
tempfile=`mktemp test19.XXXXXX`
```

---

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
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
```

# Presenting Data

Any user account on the system has privileges to read and write files in the /tmp directory. This feature provides an easy way for you to create temporary files that don't necessarily have to worry about cleaning up.

There's even specific command to use for creating a temporary file. the mktemp command allows you to easily create a unique temporary file in the /tmp folder. The shell creates the file but doesn't use your default umask value (see Chapter 6). Instead, it only assigns read and write permissions to the file's owner and makes you the owner of the file. Once you create the file, you have full access to read and write to and from it from your script, but no one else will be able to access it (other than the root user of course).

# Creating a local temporary file

By default, mktemp creates a file in the local directory. To create a temporary file in a local directory with the mktemp command, all you need to do is specify a filename template. The template consists of any text filename, fix six X's appended to the end of the filename:

```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------r 1 rich 0 Oct 29 21:30 testing.Ufii3
$
```

The mktemp command replaces the six X's with a six-character code to ensure the filename is unique in the directory. You can create multiple temporary files and be assured that each one is unique:

```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.1VBtkw
$ mktemp testing.XXXXXX
testing.PqgKG
$ ls -l testing*
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1DRLuV
-rw------- 1 rich rich 0 Oct 29 21:57 testing.PggKNG
-rw------- 1 rich rich 0 Oct 29 21:30 testing.Ufii3
-rw------- 1 rich rich 0 Oct 29 21:57 testing.1VBtkw
$
```

As you can see, the output of the mktemp command is the name of the file that it creates. When you use the mktemp command in a script, you'll want to save that filename in a variable, so you can refer to it later in the script:

```
$ cat test19
#!/bin/bash
# creating and using a temp file
tempfile=`mktemp test19.XXXXXX`
```

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
$ mkdir -t test.XXXXXX
/tmp/test.xG3374
```

# Presenting Data

Any user account on the system has privileges to read and write files in the /tmp directory. This feature provides an easy way for you to create temporary files that don't necessarily have to worry about cleaning up.

There's even specific command to use for creating a temporary file. the mktemp command allows you to easily create a unique temporary file in the /tmp folder. The shell creates the file but doesn't use your default umask value (see Chapter 6). Instead, it only assigns read and write permissions to the file's owner and makes you the owner of the file. Once you create the file, you have full access to read and write to and from it from your script, but no one else will be able to access it (other than the root user of course).
