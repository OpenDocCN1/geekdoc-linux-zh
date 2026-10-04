```
$ ls /usr/tmp >>dir
$ cat dir
total 4
drwxr-xr-x  2 pc  book  1024 May 22 23:31 bin
drwxr-xr-x  2 pc  book  1024 May 22 23:31 doc
drwxr-xr-x  2 pc  book  1024 May 22 23:31 lib
drwxr-xr-x  2 pc  book  1024 May 22 23:31 src
bin doc lib src
```

Incidentally, the cat command will take its input from the standard input device (keyboard, by default) if no file names are given as command line parameters. Input from the keyboard is terminated by entering the end-of-file character (Ctrl-d) at the start of a line on its own. Given this information, and the use of output redirection, the following simple command will allow you to write text directly from the keyboard into a file:

```
$ cat >text.file
any text entered here goes into text.file up to
Ctrl-d
$
```

As well as redirecting a program’s standard output, it is also possible to redirect its error output. The standard output and error output from a program are normally treated as two separate things so that you can redirect them individually. So, for example, if you wanted to see the normal output from a program on the screen but wanted to send any output error messages to a file so you could review them later, you could achieve this with:

```
$ ls /usr/tmp 2>err.file
bin doc lib src
```

using the notation 2> (or 2>> to append) to indicate redirection of the error output device.

In order to send both standard output and error output to the same file at the same time, another output redirection operator is used (&):

```
$ ls /usr/tmp >&output.file
```

Just as a program’s output can be written to a file, so its standard input can be read from a file instead of the keyboard. This is done with the less than (<) redirection operator:

```
$ wc </etc/passwd
     21      42      775
```

Notice that the name of the file /etc/passwd does not appear in the output from this wc command. This is because wc does not see the file name – it is dealt with