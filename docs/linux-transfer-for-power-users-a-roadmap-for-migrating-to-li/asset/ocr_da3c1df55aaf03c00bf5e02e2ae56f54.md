To create a shell script, use a text editor such as gedit (or vi or emacs, if you want to go the way of hard-core Linux users). Open the editor and type your commands, one command per line. Use the pound sign (\#) to indicate a comment.

```
```
#!/bin/bash
# My first shell script
clear
echo "Hello World!"
```
```

The first command, although marked as a comment, is a special type of comment. The “!” after the “\#” indicates that you’re identifying which shell program should execute this script, and the rest of the line points to the shell. Technically, this often isn’t necessary, because the default shell for Fedora Core is bash. But, just as it’s good programming practice to include an “otherwise” clause in a “case” structure, it’s a good idea to include the line for that one-in-a-hundred case that someone (or something) tries to run this script with another shell.

Second, save your script as “m1ss” (my first shell script) in your home directory for purposes of this example.

Third, open a command window and issue the following command:

```
`chmod 755 m1ss`
```

This changes the permissions on the file so that it can be executed. Originally, the permissions are:

```
`-rw-rw-r--`
```

The “chmod 755” command sets read/write/execute permission for the owner, read/execute permission for the group, and read/execute permission for others, like so:

```
`-rwxr-xr-x`
```

Finally, execute your shell script by typing this:

```
`./m1ss`
```

Remember, your current directory is not in your path, so you have to explicitly point to your current directory in order to run a program in it. If you just type this:

```
`m1ss`
```

you’ll get a response from the shell that says something like:

```
`bash: m1ss: command not found`
```

Assuming you’ve typed everything properly, your command window will look like this:

```
`Hello World
[which@freedoom ~] Dude?`
```