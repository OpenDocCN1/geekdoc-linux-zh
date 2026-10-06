redirection from left to right on the command line, the last example won't work properly if the stderr redirection sequence appears first on the command line

```
command 2>&> foo
```

because you will first redirect standard error to standard output then standard output to foo.

You can also dynamically redirect standard input or output in a program using the exec command:

```
exec < datafile
```

redirects standard input from the datafile. Subsequent commands executed read from standard input will read from datafile instead. The command

```
exec > /tmp/output
```

does the same thing with standard output: all commands that subsequently write standard output will write to /tmp unless explicitly redirected elsewhere.

Naturally, standard error can be reassigned as well:

```
exec 2> /tmp/errors
```

All subsequent output to standard error will go to /tmp/errors.

# <&- &&

The sequence &- has the effect of closing standard output. If preceded by a file descriptor, the associated file is closed instead. So writing

```
ls <&
```

causes the output from ls to go nowhere because standard output is closed by the shell when ls is executed. Not hugely useful, we admit!

# In-line Input Redirection

If the << characters follow a command in the format

```
command <<word
```

the shell uses the lines that follow as the input for command, until a line that contains just is found. Here's a simple example:

```
$ wc -l << ENDOFDATA
```

Use lines up to ENDOFDATA as standard input

```
> here's a line
> and another
> and yet another
> ENDOFDATA
3
```

```
$
```