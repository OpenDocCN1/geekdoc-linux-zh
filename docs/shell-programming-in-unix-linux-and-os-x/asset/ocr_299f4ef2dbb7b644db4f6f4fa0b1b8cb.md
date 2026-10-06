# Resetting Traps

After you've changed the default action to be taken on receipt of a signal, you can change it
back again with trap if you simply omit the first argument; so

```
trap HUP INT
```

resets the action to be taken on receipt of the SIGHUP or SIGINT signals back to the default
behavior for the shell.

Many shell programs also use a construct like this

```
trap /bin/rm -f $tmpfile; exit INT QUIT EXIT
```

to ensure that the rm command won't produce an error message if the temporary file hasn't
been created upon. The trap handler removes the temporary file if it exists and does
nothing if it doesn't.

# More on I/O

You know about the standard constructs <, >, >> for input redirection, output redirection,
output redirection with append, respectively. You also know that you can redirect standard
error from any command by writing 2> instead of >.

```
command 2> file
```

Sometimes you may want to explicitly write standard error in your program. With a slight
variation on the above, you can redirect standard output to standard error by writing

```
command &2
```

The notation && descriptor output redirection to a file with the file descriptor that
follows. Descriptor 0 is standard input, descriptor 1 is standard output, and descriptor 2 is
 error. It's important to remember that no space is permitted between the > and the &.

To write a message to standard error:

```
echo "Invalid number of arguments" >2
```

You may want to redirect both standard output (often abbreviated "stdout") and standard error
output ("stderr") from a program into the same file. If you know the name of the file, this is
straightforward:

```
command > foo 2>> foo
```

Here both stdout and stderr will be written to foo.

You can also write

```
command > foo 2>&1
```

to achieve the same effect; standard output is redirected to foo, and standard error is redirected
to standard output (which has already been redirected to foo). Because the shell evaluates