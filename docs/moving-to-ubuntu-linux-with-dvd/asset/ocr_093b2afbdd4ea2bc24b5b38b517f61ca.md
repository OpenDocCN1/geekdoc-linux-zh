quite wordy and you need to capture it and look at it later. Unfortunately, using the STDOUT redirect (the greater-than sign) is only going to be so useful. Error messages that are generated (such as warning messages from a compilation) go to the terminal as before. One way to deal with this is to start by redirecting STDERR to STDOUT, and then redirect that to a file. Here's the line I use for this:

```
command_name 2>&1 > logfile.out
```

Remember that file descriptor 2 is STDERR and that file descriptor 1 is STDOUT. That's what that 2>&1 construct is all about. You are redirecting fd2 to fd1 and then redirecting that output to the file of your choice. Using that program compilation example, you might wind up with something like this:

```
make -f Makefile.linux 2>&1 > compilation.output
```

> **Quick Tip** The final greater-than sign in the preceding example could be eliminated completely. When using the 2>&1 construct, it is assumed that what follows is a filename.

# The Road to Nowhere

If the command happens to be verbose by nature and doesn't have a quiet switch, you can redirect that STDOUT and STDERR noise to what longtime Linux users like to call the *bit bucket*, a special file called `/dev/null`—literally, a road to nowhere. Anything fed to the bit bucket takes up no space and is never seen or heard from again. When I was in school, we would tell people to shut up by saying, "Dev null it, will you?" As you can see, we were easily amused.

To redirect output to the bit bucket, use the STDOUT redirection.

```
command -option > /dev/null
```

If, for some strange reason, you want to sort the output of the random_names files and you do not want to see the output, you can redirect the whole thing to /dev/null in this way:

```
sort random_names > /dev/null
```