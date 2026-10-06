
## Part II Shell Scripting Basics

```
fi
$ ./test16
The first attempt failed
The second attempt succeeded
$ cat $HOME/test16
The program ran at: 20070930-1620
$
```

This is a pretty busy shell script! First, it defines a log file in your HOME directory, stores the filename of it in the variable logfile, creates the file, and then removes the write permission for the user, using the chmod command. Next, it creates the variable now and stores a timestamp, using the date command. After all of that, it checks if you have write permission to the log file (which you just took away). Since you don't have write permission, you should see the failed message appear.

After that, the script uses the chmod command again to grant the write permission back for the user, and tries to run the file. This time the script is successful.

## Checking if you can run a file

The -x comparison is a handy way to determine if you have permission for a specific script. While this may not be needed for most commands, if you run a lot of scripts from your shell scripts, it could come in:

```bash
$ cat test17
#!/bin/bash
# testing file execution
if [ -x test16 ]
then
  echo "You can run the script"
  ./test16
else
  echo "Sorry, you are unable to execute the script"
fi
$ ./test17
You can run the script:
The first attempt failed
The second attempt succeeded
$ chmod u-x test16
$ ./test17
Sorry, you are unable to execute the script
$
```

This example shell script uses the -x comparison to test if you have permission to execute the test16 script. If so, it runs the script (notice that even in a shell script, you must have the path to execute a script that's not located in your PATH). After successfully running the test16 script the first time, change the permissions on it, and try again. This time the -x comparison fails, as you don't have execute permission for the test16 script.

## Checking ownership

The -u comparison allows you to easily test if you're the owner of the file:

```bash
$ cat test18
#!/bin/bash
# check file ownership

if [ -u /etc/passwd ]
then
    echo "You're the owner of the /etc/passwd file"
else
    echo "Sorry, you're not the owner of the /etc/passwd file"
fi
$ ./test18
Sorry, you're not the owner of the /etc/passwd file
$ su
Password:
# ./test18
You're the owner of the /etc/passwd file
#
```

The script uses the -u comparison to test if the user running the script is the owner of /etc/passwd file. The first time the script runs under a normal user account, so the test fails. The second time, I used the su command to become the root user, and the test succeeded.

The -G comparison checks the default group of a file, and it succeeds if it matches the group of the default group for the user. This can be somewhat confusing, because the -G comparison only checks the default groups, and not all the groups the user belongs to. Here is an example of this:

```bash
$ cat test19
#!/bin/bash
# check file group ownership

if [ -G $HOME/testing ]
then
    echo "You're in the same group as the file"
else
    echo "The file is not owned by your group"
fi
$ ls -l $HOME/testing
-rw-rw-r-- 1 rich 58 2007-09-30 15:51 /home/testing
$ ./test19
You're in the same group as the file
$ chgrp sharing $HOME/testing
$ ./test19
The file is not owned by your group
$
```

## Part II Shell Scripting Basics

The first time the script runs, the $HOME/testing file is in the rich group, and the -G comparison succeeds. Next, I changed the group to the sharing group, which I'm also a member. However, the -G comparison failed, since it only compares the default groups, not any additional groups I belong to.

## Checking file date

The last set of comparisons deal with comparing the creation times of two files. This comes in handy when writing scripts to install software. Sometimes you don't want to install a file that is older than a file already installed on the system.

The -nt comparison determines if a file is newer than another file. If a file is newer, it will have a more recent file creation time. The -ot comparison determines if a file is older than another file. If the file is older, it will have an older file creation time:

```bash
$ cat test20
#!/bin/bash
# testing file dates

if [ ./test19 -nt ./test18 ]
then
    echo "The test19 file is newer than test18"
else
    echo "The test18 file is newer than test19"
fi

if [ ./test17 -ot ./test19 ]
then
    echo "The test17 file is older than the test19 file"
fi
$ ./test20
The test19 file is newer than test18
The test17 file is older than the test19 file
$ ls -l test17 test17
```
