# CHAPTER 3 The Command Line 81

For an almost guaranteed kill of process number 593999, issue this command:

```
[root@server ~]# kill -9 593999
```

Type the following to send the HUP signal to process number 593888:

```
[root@server ~]# kill -SIGHUP 593888
```

This command does the thing:

```
[root@server ~]# kill -1 593888
```

> TIP To getting a list of all the possible signals available, along with their numeric equivalents, issue the kill -1 command.

# Show System Name: uname

The uname program produces some system details that can be helpful in several situations. Perhaps you've managed to log into a dozen different computers remotely and have lost track of where you are! This tool is also helpful for script writers, because it allows them change the path of a script according to the system information. Here are the command-line parameters for uname:

| Option | Description |
| --- | --- |
| -m | Prints the hardware type (such as i686 for Pentium Pro and better architectures) |
| -n | Prints the machine's hostname |
| -r | Prints the operating system's release name |
| -s | Prints the operating system's release name |
| -v | Prints the operating system's version |
| -a | Prints all of the above |

To get the system's name and release, enter the following command:

```
[master@server ~]$ uname -s -r
```

The -o option might seem wasted here (after all, we know this is Linux), but this proves quite useful on old UNIX-like operating systems as well. For example, on an old Silicon Graphics, Inc. (SGI) workstation terminal, uname -s will return IRIX, and it will return SunOS on an old Sun workstation. Folks who work in heterogeneous environments often write scripts that will behave differently, depending on the OS, uname with -s is a consistent way to determine that information.