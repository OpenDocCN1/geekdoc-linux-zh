# Part II: Shell Scripting Basics

```
```
$ ./askpassword.sh
$ Enter your password:
Your password is Day31Bright-Test
$```

```

The data typed at the input prompt doesn't appear on the monitor but is assigned to the variable for use in the script.

# Reading from a file

Finally, you can also use the `read` command to read data stored in a file on the Linux system. Each call to the `read` command reads a single line of text from the file. When no more lines are left in the file, the `read` command exits with a non-0 exit status.

The tricky part is getting the data from the file to the `read` command. The most common method is to pipe (|) the result of the `cat` command of the file directly to a `while` command that contains the `read` command. Here's an example:

```
```
$ cat readfile.sh
#!/bin/bash
# Using the read command to read a file
#
count=1
cat $HOME/scripts/test.txt | while read line
do
    echo "Line $count: $line"
    count=$[ $count + 1 ]
done
    echo "Finished processing the file."
exit
$```

```

```
```
$ cat $HOME/scripts/test.txt
The quick brown dog jumps over the lazy fox.
This is a test. This is only a test.
O Romeo, Romeo! Wherefore art thou Romeo?
$```

```

```
```
$ ./readfile.sh
Line 1: The quick brown dog jumps over the lazy fox.
Line 2: This is a test. This is only a test.
Line 3: O Romeo, Romeo! Wherefore art thou Romeo?
Finished processing the file.
$```

```

The `while` command loop continues processing lines of the file with the `read` command, until the `read` command exits with a non-0 exit status.