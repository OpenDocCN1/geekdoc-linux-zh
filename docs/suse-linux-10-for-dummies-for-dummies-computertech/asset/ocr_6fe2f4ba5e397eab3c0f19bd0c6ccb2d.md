If a command is too long to fit on a single line, you can press the backslash key followed by Enter. Then, continue typing the command on the next line. For example, type the following command (press Enter after each line):

```
cat \
/etc/passwd
```

The cat command then displays the contents of the /etc/passwd file.

You can concatenate (that is, string together) several shorter commands on a single line. Just separate the commands by semicolons (;). For example, the following command

```
cd; ls -l; pwd
```

changes the current directory to your home directory, lists the contents of that directory, and then shows the name of that directory.

# Combining shell commands

You can combine simple shell commands to create a more sophisticated command. For example, suppose that you want to find out whether a device file named sbpcd resides in your system’s /dev directory because some documentation says you need that device file for a Sound Blaster Pro CD-ROM drive. You can use the ls /dev command to get a directory listing of the /dev directory, and then browse through it to see whether that listing contains sbpcd.

Unfortunately, the /dev directory has a great many entries, so you may find it hard to find any item that has sbpcd in its name. You can, however, combine the ls command with grep and come up with a command line that does exactly what you want. Here’s that command line:

```
ls /dev | grep sbpcd
```

The shell sends the output of the ls command (the directory listing) to the grep command, which searches for the string sbpcd. That vertical bar (|) is known as a pipe because it acts as a conduit (think of a water pipe) between the two programs — the output of the first command is fed into the input of the second one.

# Controlling command input and output

Most Linux commands have a common feature — they always read from the standard input (usually, the keyboard) and write to the standard output