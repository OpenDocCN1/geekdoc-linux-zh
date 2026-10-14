the program to run (see Chapter 5 [Files and Directories], page 125, for more about the path).

⇒ To run the actual ls tool with the -l option when “ls” is already defined as an alias for something, type:

```
$ /bin/ls -l [RET]
```

NOTES: When you define an alias, it only works in the current shell. To make an alias work every time you run a shell, put it in your .bashrc startup file, which is a hidden file in your home directory.

# 3.6.2 Listing Aliases

To list the aliases currently defined in your shell, simply use alias without any arguments.

⇒ To list all aliases currently defined, type:

```
$ alias [RET]
```

# 3.6.3 Removing an Alias

To remove an alias, use unalias and give the name of the alias to remove as an argument. It is removed for the duration of the shell session, unless you make the word an alias again.

⇒ To remove the alias for “ls,” type:

```
$ unalias ls [RET]
```

NOTES: If you set an alias in your .bashrc or .bash_profile file, this will remove it—but only for the current shell. To remove such an alias from all future sessions, edit the file where it is defined, and remove that particular alias line.

# 3.7 Using Shell Scripts

You know that the shell has a programming language; some of the commands that make up the Bash programming language are the ones I have been discussing in this chapter. A shell program is simply a sequence of commands for the shell to execute; a shell script is a text file that contains one. Scripts are also executable, so you can run them by typing their name as a command (see Recipe 6.3.6 [Making a File Executable], page 170).

The following recipes show how you make and run them, and how you can run special scripts automatically when you start or stop running a shell.