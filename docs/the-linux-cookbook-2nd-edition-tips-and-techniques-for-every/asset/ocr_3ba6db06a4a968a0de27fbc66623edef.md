Once you see how an alias works, you might be tempted to make an alias for everything. However, there are differences between aliases and scripts (discussed in the next section) that you should know.

With an alias, the command you run will show up in your shell history instead of the alias name you use to call it, whereas with a shell script, only the name of the script will appear and not the commands in the script. Only you can run an alias; a script, if it is put in a public bin directory, can be run by everyone on the system.

Aliases are best for calling a tool, with or without options or arguments, by another name. How to do that is shown below.

# 3.6.1 Calling a Command by Some Other Name

Use alias to assign an alias for a command; follow it with the name of the alias, an equals sign (=), and the quoted string that the alias word should represent.

⇒ To make “bye” an alias for the exit command, type:

```
$ alias bye="exit" [RET]
```

This command makes “bye” an alias for the exit tool in the current shell, so typing bye would then run exit.

You can also include options and arguments in an alias. When you do, be sure to enclose the entire alias in double quotes.

⇒ To make “ls” an alias for the command to list a directory in color on terminals that allow color display, type:

```
$ alias ls="ls --color=auto" [RET]
```

This command makes “ls” an alias for the ls file listing tool with its --color=auto option specified, which sets color when the output is directed to a terminal that is capable of displaying it.

This is a common alias, and many Linux systems come preconfigured with it in the default .bashrc file. It’s also common to make “l” an alias for ls with the -l option (see Recipe 5.3.3 [Listing File Attributes], page 136).

When you have this alias defined you can still pass other options to ls just by specifying them; so typing ls -l in this case will execute ls --color=auto -l as the actual command.

Aliases are always expanded before the shell looks on your path, so to run a tool or program whose name is also an alias, give the full path name of