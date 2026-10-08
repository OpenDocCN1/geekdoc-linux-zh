| Features | Description |
| --- | --- |
| bash | BASH shell, /bin/bash |
| bsh | BASH shell, /bin/bsh (link to /bin/bash) |
| sh | BASH shell, /bin/sh (link to /bin/bash) |
| tcsh | TCSH shell, /usr/tcsh |
| csh | TCSH shell, /bin/csh (link to /bin/tcsh) |
| ksh | Korn shell, /bin/ksh (also added link /usr/bin/ksh) |
| zsh | Z shell, /bin/zsh |

**TABLE 9-1** Shell Invocation Command Names

# # Aliases

You use the **alias** command to create another name for a command. The **alias** command operates like a macro that expands to the command it represents. The alias does not literally replace the name of the command; it simply gives another name to that command. An **alias** command begins with the keyword **alias** and the new name for the command, followed by an equal sign and the command the alias will reference.

**NOTE** No spaces can be around the equal sign used in the *alias* command.

In the next example, **list** becomes another name for the **ls** command:

```
```
$ alias list=ls
$ ls
mydata today
$ list
mydata today
$ 
```
```

# ## Aliasing Commands and Options

You can also use an alias to substitute for a command and its option, but you need to enclose both the command and the option within single quotes. Any command you alias that contains spaces must be enclosed in single quotes. In the next example, the alias **lss** references the **ls** command with its **-s** option, and the alias **lsa** references the **ls** command with the **-F** option. The **ls** command with the **-s** option lists files and their sizes in blocks, and **ls** with the **-F** option places a slash after directory names. Notice how single quotes enclose the command and its option.

```
```
$ alias lss='ls -s'
$ lss
mydata 14 today 6 reports 1
$ alias lsa='ls -F'
$ lsa
mydata today reports/
$ 
```
```