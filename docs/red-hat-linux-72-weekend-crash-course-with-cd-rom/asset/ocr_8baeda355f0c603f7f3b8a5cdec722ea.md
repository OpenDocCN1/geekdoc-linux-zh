The number and format of the command-line options, of course, depend on the actual command. As you learn more commands, you will see that most of the command-line options take the form -X in which *X* is a single character.

![](bbox=[0.08, 0.15, 0.14, 0.2])

Because various GNU tools and utilities implement most Linux commands, you should know that GNU command support includes so-called long options. These are command-line options that begin with two dashes followed by one or more descriptive words. Thus, the GNU options take the form --xxxx in which xxxx is a word denoting the option. For example, the `ls --all` command shows all directory entries including those that *begin* with a period (.). This is the same as the `ls -a` command in all UNIX systems.

If a command is too long to fit on a single line, you can press the backslash (\) key, followed by Enter. Then, continue entering the command on the next line. For example, type the following command (press Enter after each line):

```
cat \
/etc/passwd
```

The `cat` command then displays the contents of the /etc/passwd file.

You can concatenate several shorter commands on a single line; just use the semicolon (;) as a separator (also called a command *terminator*) between each command. For example, the following command

```
cd ; ls -F
```

changes the current directory to your home directory and then lists the contents of that directory.

# ### Getting help with Bash

Bash comes with many built-in commands, some of which mimic or duplicate the functionality of other programs on your Red Hat Linux system. To see the complete list of these Bash built-ins, as they are called, type `help` and press Enter at the Bash command prompt. To get help with a specific Bash built-in, type `help *command*`, where *command* is the Bash command about which you want to learn. For example, type the following command and then press Enter

```
help pwd
```

The short help text shows the syntax of Bash’s built-in command `pwd`, briefly describes what it does, and provides an explanation of pwd’s command-line options:

```
pwd [-P|-L]
Print the current working directory.  With the -P option,
pwd prints the physical directory, without any symbolic
links; the -L option makes pwd follow symbolic links.
```

The exact appearance on your system will be different because the output shown here has been edited to fit this book’s formatting requirements.