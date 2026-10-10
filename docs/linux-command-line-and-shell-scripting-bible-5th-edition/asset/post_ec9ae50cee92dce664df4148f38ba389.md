
## Part II: Shell Scripting Basics

This shows the default file descriptors (0, 1, and 2) for the current process (the Bash shell). The default output of `lsof` contains several columns of information, described in Table 15.2.

### TABLE 15.2 Default `lsof` Output

| Column | Description |
| :--- | :--- |
| COMMAND | The first nine characters of the name of the command in the process |
| PID | The process ID of the process |
| USER | The login name of the user who owns the process |
| FD | The file descriptor number and access type (r (read), w (write), u (read/write)) |
| TYPE | The type of file (CHR (character), BLK (block), DIR (directory), REG (regular file)) |
| DEVICE | The device numbers (major and minor) of the device |
| SIZE | If available, the size of the file |
| NODE | The node number of the local file |
| NAME | The name of the file |

The file type associated with STDIN, STDOUT, and STDERR is character mode. Because the STDIN, STDOUT, and STDERR file descriptors all point to the terminal, the name of the output file is the device name of the terminal. All three standard files are available for both reading and writing (although it does seem odd to be able to write to STDIN and read from STDOUT).

Now, let’s look at the results of the `lsof` command from inside a script that’s opened a couple of alternative file descriptors:

```bash
$ cat test18
#!/bin/bash
# testing lsof with file descriptors

exec 3> test18file1
exec 6> test18file2
exec 7< testfile

lsof -a -p $$ -d0,1,2,3,6,7
$ ./test18
COMMAND  PID USER   FD  TYPE DEVICE SIZE     NODE NAME
test18   3594 rich   0u   CHR  136,0        2 /dev/pts/0
test18   3594 rich   1u   CHR  136,0        2 /dev/pts/0
test18   3594 rich   2u   CHR  136,0        2 /dev/pts/0
test18   3594 rich   3w   REG  253,0     0 18 /home/rich/test18file1
test18   3594 rich   6w   REG  253,0     0 11 /home/rich/test18file2
test18   3594 rich   7r   REG  253,0    73 33 /home/rich/testfile
$ 
```

The script creates three alternative file descriptors, two for output (3 and 6) and one for input (7). When the script runs the `lsof` command, you can see the new file descriptors in the output. The filename shows the complete pathname for the files used in the file descriptors. It shows each of the files as type REG, which indicates that they are regular files on the filesystem.

## Suppressing Command Output

Sometimes, you may not want to display any output from your script. This often occurs if you’re running a script as a background process (see Chapter 16, “Script Control”). If any error messages occur from the script while it’s running in the background, the shell emails them to the owner of the process. This can get tedious, especially if you run scripts that generate minor nuisance errors.

To solve that problem, you can redirect `STDERR` to a special file called the `null file`. The null file is pretty much what it says it is—a file that contains nothing. Any data that the shell outputs to the null file is not saved; thus, the data is lost.

The standard location for the null file on Linux systems is /dev/null. Any data you redirect to that location is thrown away and doesn’t appear:

```bash
$ ls -al > /dev/null
$ cat /dev/null
$
```

This is a common way to suppress any error messages without actually saving them:

```bash
$ ls -al badfile test16 2> /dev/null
-rw-r--r-- 1 rich rich 135 Jun 20 19:57 test16
$
```

You can also use the /dev/null file for input redirection as an input file. Because the /dev/null file contains nothing, it is often used by programmers to quickly remove data from an existing file without having to remove the file and re-create it:

```bash
$ cat testfile
This is the first line.
This is the second line.
This is the third line.
$ cat /dev/null > testfile
$ cat testfile
$
```

The file `testfile` still exists on the system, but now it is empty. This is a common method used to clear out log files that must remain in place for applications to operate.

## Using Temporary Files

The Linux system contains a special directory location reserved for temporary files. Linux uses the `/tmp` directory for files that don’t need to be kept indefinitely. Most Linux distributions configure the system to automatically remove any files in the `/tmp` directory at bootup.

Any user account on the system has privileges to read and write files in the /tmp directory. This feature provides an easy way for you to create temporary files that you don’t necessarily have to worry about cleaning up.

There’s even a specific command to use for creating a temporary file. The `mktemp` command allows you to easily create a unique temporary file in the `/tmp` folder. The shell creates the file but doesn’t use your default `umask` value (see Chapter 7, “Understanding Linux File Permissions”). Instead, it only assigns read and write permissions to the file’s owner and makes you the owner of the file. After you create the file, you have full access to read and write to and from it from your script, but no one else can access it (other than the root user, of course).

### Creating a local temporary file

By default, `mktemp` creates a file in the local directory. To create a temporary file in a local directory with the `mktemp` command, you just need to specify a filename template. The template consists of any text filename, plus six X’s appended to the end of the filename:

```bash
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------    1 rich       rich       0 Jun 20 21:30 testing.Uffff33
$ 
```

The `mktemp` command replaces the six X’s with a six-character code to ensure that the filename is unique in the directory. You can create multiple temporary files and be assured that each one is unique:

```bash
$ mktemp testing.XXXXXX
testing.1DRluV
$ mktemp testing.XXXXXX
testing.1vBtkW
$ mktemp testing.XXXXXX
testing.PggNKG
$ ls -l testing*
-rw-------    1 rich       rich       0 Jun 20 21:57 testing.1DRluV
-rw-------    1 rich       rich       0 Jun 20 21:57 testing.PggNKG
-rw-------    1 rich       rich       0 Jun 20 21:30 testing.Uffff33
-rw-------    1 rich       rich       0 Jun 20 21:57 testing.1vBtkW
$ 
```

As you can see, the output of the `mktemp` command is the name of the file that it creates. When you use the `mktemp` command in a script, you’ll want to save that filename in a variable so that you can refer to it later on in the script:

```bash
$ cat test19
#!/bin/bash
# creating and using a temp file

tempfile=$(mktemp test19.XXXXXX)

exec 3>tempfile

echo "This script writes to temp file $tempfile"

echo "This is the first line" >&3
echo "This is the second line." >&3
echo "This is the last line." >&3
exec 3>&-

echo "Done creating temp file. The contents are:"
cat $tempfile
rm -f $tempfile 2> /dev/null
$ ./test19
This script writes to temp file test19.vCDoYa
Done creating temp file. The contents are:
This is the first line.
This is the second line.
This is the last line.
$ ls -al test19*
-rwxr--r-- 1 rich rich 356 Jun 20 22:03 test19
$ 
```

The script uses the mktemp command to create a temporary file and assigns the filename to the `tempfile` variable. It then uses the temporary file as the output redirection file for file descriptor 3. After displaying the temporary filename on STDOUT, it writes a few lines to the temporary file, and then it closes the file descriptor. Finally, it displays the contents of the temporary file and then uses the rm command to remove it.

## Creating a temporary file in /tmp

The -t option forces mktemp to create the file in the temporary directory of the system. When you use this feature, the mktemp command returns the full pathname used to create the temporary file, not just the filename:

```bash
$ mktemp -t test.XXXXXX
/tmp/test.xG3374
$ ls -al /tmp/test*
-rw------- 1 rich rich 0 2025-06-20 18:41 /tmp/test.xG3374
$ 
```

Because the mktemp command returns the full pathname, you can then reference the temporary file from any directory on the Linux system, no matter where it places the temporary directory:

```bash
$ cat test20
#!/bin/bash
# creating a temp file in /tmp

tempfile=$(mktemp -t tmp.XXXXXX)

echo "This is a test file." > $tempfile
echo "This is the second line of the test." >> $tempfile
```
