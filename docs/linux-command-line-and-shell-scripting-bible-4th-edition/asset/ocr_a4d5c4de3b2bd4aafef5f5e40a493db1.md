```
echo "Sorry, the $item_name does not exist"
echo "or is not a file."
fi
$
$ ls -o $HOME/sentinel
-rw-rw-r-- 1 christine 32 May 25 17:08
/home/christine/sentinel
$
$ ./can-I-write-to-it.sh
Checking if you can write to /home/christine/sentinel...
Writing current time to /home/christine/sentinel
$
```

The item_name variable is set to $HOME/sentinel, and this file allows user write access (see Chapter 7, “Understanding Linux File Permissions,” for more information on file permissions). Thus, when the script is run, the -w test expression returns a non-zero exit status and the then code block is executed, which writes a time stamp into the sentinel file.

When the sentinel file user’s write access is removed via chmod, the -w test expression returns a non-zero status, and a time stamp is not written to the file:

```
$ chmod u-w $HOME/sentinel
$
$ ls -o $HOME/sentinel
-r---rw-r-- 1 christine 37 May 29 12:07
/home/christine/sentinel
$
$ ./can-I-write-to-it.sh
Checking if you can write to /home/christine/sentinel...
Sorry, write access to /home/christine/sentinel is denied.
$
```

The chmod command could be used again to grant the write permission back for the user. This would make the write test expression return a zero exit status and allow a write attempt to the file.

# Checking whether you can run a file

The -x comparison is a handy way to determine whether you have execute permission for a specific file. Although this may not be needed