![](bbox=[0.07, 0.14, 0.2, 0.22])

In the output from the grep command, you can see the name of the shell (/bin/bash) following the last colon (:).

The number and the format of the command-line options, of course, depend on the actual command. When you learn more about the commands, you see that the command-line options controlling the behavior of a command usually take the form -X in which X is a single character.

![](bbox=[0.07, 0.31, 0.2, 0.4])

Because various GNU tools and utilities implement most Linux commands, you should know that GNU command-line options begin with two dashes followed by a descriptive word. Thus, the GNU options take the form --xxxx in which xxxx is a word denoting the option. For example, the GNU ls --all command shows all directory entries including those that begin with a period (.). This is the same as the ls -a command in all UNIX systems.

If a command is too long to fit on a single line, you can press the backslash (\ ) key, followed by Enter. Then, continue entering the command on the next line. For example, type the following command (press Enter after each line):

```
cat \
/etc/passwd
```

The cat command then displays the contents of the /etc/passwd file.

You can concatenate several shorter commands on a single line; just use the semicolon (;) as a separator between the commands. For example, the following command

```
cd; ls -F
```

changes the current directory to your home directory and then lists the contents of that directory.

# Combining commands

Linux follows the UNIX philosophy of giving the user a toolbox of many simple commands. You can, however, combine these simple commands to create a more sophisticated command. Suppose you want to find out whether a device file named sbpcd resides in your system's /dev directory because some documentation tells you that for a Sound Blaster Pro CD-ROM drive, you need that device file. You can