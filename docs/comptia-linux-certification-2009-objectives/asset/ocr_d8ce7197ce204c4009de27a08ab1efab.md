# Argument

An *argument*, also called command line argument, is usually a file name or directory name that indicates the files on which the command will operate. It is used as an input by some com-mands in Linux. Arguments can be files, directories, commands or even a command switch. For example, `ls (file_name)`, `ls (directory_name)`, and `ls -l`.

# Command History

Sometimes, commands can become quite long. You can access previously entered commands that are stored in the History file by using the **Up Arrow** and the **Down Arrow** keys.

# The Tab-Completion Feature

Some commands have long names containing version number information, weird spellings, or capitalizations. This can make it difficult to correctly enter the commands on the first try. In such a case, you can make use of the tab-completion feature. To use this feature, enter the first few characters of the command and then press the **Tab** key. If there is only one match, the rest of the file name is displayed. If you press the next letter of the file name you want and press the **Tab** key again, the complete file name should come up. If the system still cannot differentiate between the commands, it will beep again, and you have to enter additional characters or press the **Tab** key two times to view all available options.

# Issuing More Than One Command

You can issue more than one command before pressing **Enter**. Place a semicolon (`;`) between the commands and they will be issued one after the other.

# The date Command

The `date` command displays the current date and time set on a system. You can use the hyphen (`-`) or the colon (`:`) between the different fields of the date for a clear output.

![](bbox=[0.74, 0.49, 0.85, 0.56])

```
The date command
root@localhost:~# date
Wed Jun 24 07:59:43 EDT 2009
root@localhost:~#
```

*Figure 1-10: Viewing the current date using the date command.*