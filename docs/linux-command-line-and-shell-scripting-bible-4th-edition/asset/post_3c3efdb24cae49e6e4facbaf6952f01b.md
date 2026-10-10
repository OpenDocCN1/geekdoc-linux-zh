
```bash
read -p "Are you done now? " answer
case $answer in
Y[y]*) echo "Goodbye";;
N[n]*) echo "Sorry, this is the end.";;
esac
$ ./test15
Line #1: This is the first line.
Line #2: This is the second line.
Line #3: This is the third line.
Are you done now? y
Goodbye
$
```

In this example, file descriptor 6 is used to hold the location for STDIN. The script then redirects STDIN to a file. All the input for the `read` command comes from the redirected STDIN, which is now the input file.

When all the lines have been read, the script returns STDIN to its original location by redirecting it to file descriptor 6. The script tests to make sure that STDIN is back to normal by using another `read` command, which this time waits for input from the keyboard.

### Creating a read/write file descriptor

As odd as it may seem, you can also open a single file descriptor for both input and output. You can then use the same file descriptor to both read data from a file and write data to the same file.

You need to be especially careful with this method, however. As you read and write data to and from a file, the shell maintains an internal pointer, indicating where it is in the file. Any reading or writing occurs where the file pointer last left off. This can produce some interesting results if you're not careful. Look at this example:

```bash
$ cat test16
#!/bin/bash
# testing input/output file descriptor

exec 3<> testfile
read line <&3
echo "Read: $line"
echo "This is a test line">&3
$ cat testfile
This is the first line.
This is the second line.
This is the third line.
$ ./test16
Read: This is the first line.
$ cat testfile
This is the first line.
This is a test line
ine.
This is the third line.
$
```

This example uses the `exec` command to assign file descriptor 3 for both input and output sent to and from the file `testfile`. Next, it uses the `read` command to read the first line in the file, using the assigned file descriptor, and then it displays the read line of data in `STDOUT`. After that, it uses the `echo` statement to write a line of data to the file opened with the same file descriptor.

When you run the script, at first things look just fine. The output shows that the script read the first line in the `testfile` file. However, if you display the contents of the `testfile` file after running the script, you see that the data written to the file overwrote the existing data.

When the script writes data to the file, it starts where the file pointer is located. The `read` command reads the first line of data, so it left the file pointer pointing to the first character in the second line of data. When the `echo` statement outputs data to the file, it places the data at the current location of the file pointer, overwriting whatever data was there.

## Closing file descriptors

If you create new input or output file descriptors, the shell automatically closes them when the script exits. There are situations, however, when you need to manually close a file descriptor before the end of the script.

To close a file descriptor, redirect it to the special symbol `&-`. This is how it looks in the script:

```bash
exec 3>&-
```

This statement closes file descriptor 3, preventing it from being used any more in the script. Here's an example of what happens when you try to use a closed file descriptor:

```bash
$ cat badtest
#!/bin/bash
# testing closing file descriptors

exec 3> test17file

echo "This is a test line of data">&3

exec 3>&-

echo "This won't work">&3
$ ./badtest
./badtest: 3: Bad file descriptor
$
```

After you close the file descriptor, you can't write any data to it in your script or the shell produces an error message.

There's yet another thing to be careful of when closing file descriptors. If you open the same output file later on in your script, the shell replaces the existing file with a new file. This means that if you output any data, it overwrites the existing file. Consider the following example of this problem:

```bash
$ cat test17
#!/bin/bash
# testing closing file descriptors

exec 3> test17file
echo "This is a test line of data">&3
exec 3>&-

cat test17file

exec 3> test17file
echo "This'll be bad">&3
$ ./test17
This is a test line of data
$ cat test17file
This'll be bad
$
```

After sending a data string to the test17file file and closing the file descriptor, the script uses the `cat` command to display the contents of the file. So far, so good. Next, the script reopens the output file and sends another data string to it. When you display the contents of the output file, all you see is the second data string. The shell overwrote the original output file.

### Listing Open File Descriptors

With only nine file descriptors available to you, you’d think that it wouldn’t be hard to keep things straight. Sometimes, however, it’s easy to get lost when trying to keep track of which file descriptor is redirected where. To help you keep your sanity, the Bash shell provides the `lsof` command.

The `lsof` command lists all the open file descriptors on the entire Linux system. This includes files open by all the processes running in the background, as well as any user accounts logged in to the system.

Plenty of command-line parameters and options are available to help filter out the `lsof` output. The most commonly used are `-p`, which allows you to specify a process ID (PID), and `-d`, which allows you to specify the file descriptor numbers to display, separated by commas.

To easily determine the current PID of the process, you can use the special environment variable `$$`, which the shell sets to the current PID. The `-a` option is used to perform a Boolean AND of the results of the other two options, to produce the following:

```bash
$ /usr/sbin/lsof -a -p $$ -d 0,1,2
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
bash 3344 rich 0u CHR 136,0 2 /dev/pts/0
bash 3344 rich 1u CHR 136,0 2 /dev/pts/0
bash 3344 rich 2u CHR 136,0 2 /dev/pts/0
$
```

This shows the default file descriptors (0, 1, and 2) for the current process (the Bash shell). The default output of `lsof` contains several columns of information, described in Table 15-2.

## TABLE 15-2 Default lsof Output

| Column | Description |
| :--- | :--- |
| COMMAND | The first nine characters of the name of the command in the process |
| PID | The process ID of the process |
| USER | The login name of the user who owns the process |
| FD | The file descriptor number and access type (r – [read], w – [write], u – [read/write]) |
| TYPE | The type of file (CHR – [character], BLK – [block], DIR – [directory], REG – [regular file]) |
| DEVICE | The device numbers (major and minor) of the device |
| SIZE | If available, the size of the file |
| NODE | The node number of the local file |
| NAME | The name of the file |

The file type associated with **STDIN**, **STDOUT**, and **STDERR** is character mode. Because the **STDIN**, **STDOUT**, and **STDERR** file descriptors all point to the terminal, the name of the output file is the device name of the terminal. All three standard files are available for both reading and writing (although it does seem odd to be able to write to **STDIN** and read from **STDOUT**).

Now, let’s look at the results of the `lsof` command from inside a script that’s opened a couple of alternative file descriptors:

```bash
$ cat test18
#!/bin/bash
# testing lsof with file descriptors

exec 3> test18file1
exec 6> test18file2
exec 7> testfile

/usr/sbin/lsof -a -p $$ -d0,1,2,3,6,7
$ ./test18
COMMAND PID USER    FD TYPE DEVICE SIZE     NODE NAME
test18  3594 rich   0u  CHR  136,0          2 /dev/pts/0
test18  3594 rich   1u  CHR  136,0          2 /dev/pts/0
test18  3594 rich   2u  CHR  136,0          2 /dev/pts/0
test18  3594 rich     3w  REG  253,0   0 360712
/home/rich/test18file1
test18  3594 rich 6w REG 253,0 0 360715
/home/rich/test18file2
test18  3594 rich 7r REG 253,0 73 360717
/home/rich/testfile
$
```

The script creates three alternative file descriptors, two for output (3 and 6) and one for input (7). When the script runs the `lsof` command, you can see the new file descriptors in the output. We truncated the first part of the output so that you could see the results of the filename. The filename shows the complete pathname for the files used in the file descriptors. It shows each of the files as type `REG`, which indicates that they are regular files on the filesystem.

### Suppressing Command Output

Sometimes, you may not want to display any output from your script. This often occurs if you're running a script as a background process (see Chapter 16, “Script Control”). If any error messages occur from the script while it's running in the background, the shell emails them to the owner of the process. This can get tedious, especially if you run scripts that generate minor nuisance errors.

To solve that problem, you can redirect `STDERR` to a special file called the null file. The null file is pretty much what it says it is—a file that contains nothing. Any data that the shell outputs to the null file is not saved, thus the data is lost.

The standard location for the null file on Linux systems is `/dev/null`. Any data you redirect to that location is thrown away and doesn't appear:

```bash
$ ls -al > /dev/null
$ cat /dev/null
$
```

This is a common way to suppress any error messages without actually saving them:

```bash
$ ls -al badfile test16 2> /dev/null
-rwxr--r-- 1 rich rich 135 Jun 20 19:57
```
