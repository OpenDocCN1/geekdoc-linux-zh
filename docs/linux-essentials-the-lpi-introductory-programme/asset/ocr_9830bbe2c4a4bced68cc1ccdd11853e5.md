# ## 9.5 Commands From A File

You can store shell commands in a file and execute *en bloc*. (You will learn how to create a file conveniently in Chapter 3.) You just need to invoke the shell and pass the file name as a parameter:

```
`$ bash my-commands`
```

Such a file is also called a **shell script**, and the shell has extensive programming features that we can only outline very briefly here. (The Linup Front training manual *Advanced Linux* explains shell programming in great detail.)

💡 You can avoid having to prepend the *bash* command by inserting the magical incantation

```
`#!/bin/bash`
```

as the first line of your file and making the file “executable”:

```
`$ chmod +x my-commands`
```

(You will find out more about `chmod` and access rights in Chapter 14.) After this, the

```
`$ ./my-commands`
```

command will suffice.

If you invoke a shell script as above, whether with a prepended *bash* or as an executable file, it is executed in a *subshell*, a shell that is a child process of the current shell. This means that changes to, *e.g.*, shell or environment variables do not influence the current shell. For example, assume that the file *assignment* contains the line

```
`foo=bar`
```

Consider the following command sequence:

```
$ foo=quux
$ bash assignment          Contains foo=bar
$ echo $foo
quux                       No change; assignment was only in subshell
```

This is generally considered a feature, but every now and then it would be quite desirable to have commands from a file affect the *current* shell. That works, too: The *source* command reads the lines in a file exactly as if you would type them directly into the current shell—all changes to variables (among other things) hence take effect in your current shell:

```
$ foo=quux
$ source assignment        Contains foo=bar
$ echo $foo
bar                        Variable was changed!
```

A different name for the *source* command, by the way, is *.* (You read correctly – dot!) Hence

```
`$ source assignment`
```