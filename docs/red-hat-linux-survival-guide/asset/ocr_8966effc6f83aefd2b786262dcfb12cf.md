To see the list of all environment variables, run set by itself. To view the value of a specific environment variable, such as path, run:

```
echo $path
```

This shows you the value of the named environment variable. If you use this command quite often to set a few special environment variables, you can add it to .login or .profile or to your shell’s dot file in your home directory so that the special environment variables are automatically set when you log in.

# source

Syntax: source filename

This is a built-in shell command available in most popular shells. This command lets you read and execute commands from the named file in the current shell environment.

# unalias

Syntax: unalias name of the alias

This is a built-in shell command that’s available in most popular shells that lets you remove an alias for a command. For example, the following command removes an alias called dir:
unalias dir
To remove all aliases, use “*” as the argument.

# Printing-Specific Commands

This section discusses commands that help you print from your Linux system. Using these commands you can view the print queue status, print files, or remove print jobs from the current print queue.

# lpq

Syntax: lpq [-al] [-P printer]