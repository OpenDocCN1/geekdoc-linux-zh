# Chapter 2 + Running Commands from the Shell 49

a typed character that has special meaning to the shell for connecting commands
or requesting expansion.

# Piping Commands

The pipe() metacharacter connects the output from one command to the input of
another command. This lets you have one macro work on some data, and then
have the next command deal with the results. Here is an example of a command line
that includes pipes:

```
$ /etc/password | sort | less
```

This command lists the contents of the /etc/password file and pipes the output to
t sort command. The sort command takes usernames that begin each line
of the /etc/password file, sorts them alphabetically, and pipes the output to the
less command through the output.

Pipes are an excellent illustration of how UNIX, the predecessor of Linux, was cre-
ated as an operating system made of building blocks. A standard practice in
IX was to connect utilities in different ways to get different jobs done. For exam-
ple days of graphical word processors, users created plain-text files that
included macros to indicate formatting. See how the document really appeared,
by they would use gunzip as the following:

```
$ gunzip < /usr/share/man/man1/grep.gz nroff c man less
```

In this example, the grep page (grep.gz) are directed to the
gunzip command to be unzipped. The output from gunzip is piped to the nroff
command to format the page using the manual macro (-man). The output is
piped to in plain text, you could have substituted any number of options to work with the
text before displaying it. You could use the contents, change or delete some of the
content, or bring in text from other documents. The key is that, instead of all those
features in one program, you get results from piping and redirecting input
over multiple commands.

# Sequential Commands

Sometimes you may want a sequence of commands to run, with one command com-
pleting the first command begins. You can do this by typing several com-
mands the same command and separating them with semicolons ();

```
$ date ; troff - me verylargedocument | lpr : date
```

In this example, I was formatting a document and wanted to know how long it
would take. The first command (date) showed the date and time before the format-
started. The troff command formatted the document and piped the out-
p the printer. When the formatting was done, the date and time was printed
again (so I knew how long the troff command took to complete).