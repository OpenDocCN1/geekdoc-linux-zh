# Part II Shell Scripting Basics

This script does a whole lot of checking! First, it uses the -e comparison to test if $HOME exists. If it isn't a file, it uses -f to test if it's a file (which of course it isn't), we use the -f comparison to test if it's a file, which it is.

# Can you read it?

Before trying to read data from a file, it's usually a good idea to test if you can read from the file. First this is done using the -r comparison:

```
$ cat test14
#!/bin/bash
# testing if you can read a file
pwfile=/etc/shadow

# first, test if the file exists, and is a file
if [ -f $pwfile ];
then
    # now test if you can read it
    if [ -r $pwfile ];
then
        tail $pwfile
    else
        echo "Sorry, I'm unable to read the $pwfile"
fi
else
    echo "Sorry, the $file doesn't exist"
fi
$ ./test14
Sorry, I'm unable to read the /etc/shadow file
```

The /etc/shadow file contains the encrypted passwords for system users, so it's not readable by normal users on the system. The -r comparison determined that I didn't have access to the file, so the test command failed, and the bash shell executed the section of the if-then statement.

# Checking for empty files

You should use -s comparison to check if a file is empty, especially if you're trying to remove a file. Be careful, because when the -s comparison succeeds, it indicates that a file has data in it:

```
$ cat test15
#!/bin/bash
# testing if a file is empty
file=t15test
touch $file
```

```
if [ -s $file ];
then
```