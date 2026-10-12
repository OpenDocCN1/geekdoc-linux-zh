# Moving Files with mv

This command is one of the easiest around. There are two helpful parameters to *mv*: *-f*, which overwrites files without asking, and *-u*, which moves the source file only if it is newer than the destination file. That is it!

# Listing Processes with ps

This is the third and last “command that should be simple, but isn’t” that is discussed here. The *ps* command lists processes and gives you an extraordinary amount of control over its operation.

The first thing to know is that *ps* is typically used with what are known as BSD-style parameters. Back in the section “Finding Files with *find*,” we discussed Unix-style, GNU-style, and X-style parameters (*-c*, *--dosomething*, and *-dosomething*, respectively), but BSD-style parameters are different because they use single letters without a dash.

So, the default use of *ps* lists all processes that you are running that are attached to the terminal. However, you can ask it to list all your processes attached to any terminal (or indeed no terminal) by adding the x parameter: `ps x`. You can ask it to list all processes for all users with the a parameter or combine that with x to list all processes for all users, attached to a terminal or otherwise: `ps ax`.

However, both of these are timid compared with the almighty u option, which enables user-oriented output. In practice, that makes a huge difference because you get important fields like the username of the owner, how much CPU time and RAM are being used, when the process was started, and more. This outputs a lot of information, so you might want to try adding the f parameter, which creates a process forest by using ASCII art to connect parent commands with their children. You can combine all the options so far with this command: `ps faux` (yes, with a little imagination you spell words with the parameters!)

You can control the order in which the data is returned by using the `--sort` parameter. This takes either a + or a - (although the + is default) followed by the field you want to sort by: *command*, *%cpu*, *pid*, and *user* are all popular options. If you use the minus sign, the results are reversed. This next command lists all processes, ordered by CPU usage descending:

```
```
ps aux --sort=-%cpu
```
```

There are many other parameters for *ps*, including a huge amount of options for compatibility with other Unixes. If you have the time to read the man page, you should give it a try!

# Deleting Files and Directories with rm

The *rm* command has only one parameter of interest: *--preserve-root*. By now, you should know that issuing `rm -rf /` as root will destroy your Linux installation because *-r* means *recursive* and *-f* means *force* (do not prompt for confirmation before deleting). It is

![](bbox=[0.95, 0.41, 0.98, 0.5])