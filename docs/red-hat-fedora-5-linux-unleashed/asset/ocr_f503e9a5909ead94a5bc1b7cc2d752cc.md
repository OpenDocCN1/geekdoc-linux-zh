# Deleting Files and Directories with rm

The rm command has only one parameter of interest: --preserve-root. By now, you should know that issuing rm -rf / as root will destroy your Linux installation because -r means recursive and -f means force (do not prompt for confirmation before deleting). It is possible for a clumsy person to issue this command by accident—not by typing the command on purpose, but by putting a space in the wrong place. For example:

```
rm -rf / home/paul
```

That command deletes the home directory of the user paul. This is not an uncommon command; after you removed a user and backed up her data, you will probably want to issue something similar. However, if you add an accidental space between the / and the h in home, you get this:

```
rm -rf / home/paul
```

This time the command means “delete everything recursively from / and then delete home/paul” —quite a different result! You can stop this from happening by using the --preserve-root parameter, which stops you from catastrophe with this message:

```
rm: it is dangerous to operate recursively on '/'
rm: use --no-preserve-root to override this failsafe.
```

Of course, no one wants to keep typing --preserve-root each time they run rm, so you should add this line to the .bashrc file in your home directory:

```
alias rm='rm --preserve-root'
```

That alias automatically adds --preserve-root to all calls to rm in future bash sessions.

# Printing the Last Lines of a File with tail

If you want to watch a log file as it is written to, or want to monitor a user’s actions as they are occurring, you need to be able to track log files as they change. In these situations you need the tail command, which prints the last few lines of a file and updates as new lines are added. This command tells tail to print the last few lines of /var/log/httpd/access_log, the Apache hit log:

```
tail /var/log/httpd/access_log
```

To get tail to remain running and update as the file changes, add the -f parameter (which means “follow”):

```
tail -f /var/log/httpd/access_log
```

You can tie the lifespan of a tail follow to the existence of a process by specifying the -pid parameter. When you do this, tail continues to follow the file you asked for until it sees that the process (identified by PID) is no longer running, at which point tail stops tailing.