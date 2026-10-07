pleted successfully or not, but when you don't care about its output. (A similar device, /dev/zero, contains an infinite supply of null bytes.)

Enter the following command lines:

```
if grep "^$(USER):" /etc/passwd > /dev/null
then print "You have a local account on this system."
else print "You have a network account for accessing this system."
fi
```

a) What does this statement do, and why is the output of the grep command redirected to /dev/null?

The second one, /dev/tty, represents the user's terminal, no matter what has happened to stdout and stderr.

Enter the following command in a script named insist:

```
print "Hey, pay attention to me!" > /dev/tty
```

Now invoke the script as follows:

```
insist > /dev/null 2>&1
```

b) What does the I/O redirection on the command line do?

c) Did the "pay attention" message print on the screen?