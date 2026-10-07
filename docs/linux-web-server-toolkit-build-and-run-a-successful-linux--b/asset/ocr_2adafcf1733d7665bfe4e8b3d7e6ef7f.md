# Chapter 4: Internet and UNIX Technologies

things from a graphical interface such as your browser or the OpenLinux Lite Desktop. But you should still have some familiarity with command-line tools.

Whenever you want to learn about a command, system file, options, and so on, you can quickly view the UNIX manual page to read about it. To do this, use the man command with the name of the command or file that you want to read about. The man command is a viewer for online manual pages. For example, if you want to know about the ps command described previously, enter the following command:

```
man ps
```

If you want to know about the options shown in this chapter for the ls command (used to list files), enter the following command:

```
man ls
```

These man pages are usually written by the author of the utility, so they can be quite technical. In addition, even the common utilities in Linux (ls being an immediate example) have so many options that you may feel a little overwhelmed trying to complete a simple task until you get a feel for the organization of the manual pages. Just don't try to learn all the options at one time! The manual pages are made easily accessible so that you can refer back to them at any time.

Some UNIX commands that you want to try once your Linux system is installed are shown in Table 4-8. Note that all command names, filenames, and directory names are case-sensitive in Linux. Entering the commands more, More, and MORE will access three different files, only one of which is a standard command.

# Table 4-8 Key UNIX Commands

| Command | Description | Example(s) |
| --- | --- | --- |
| cp | Copies a file from one location to another. Like the DOS command, but you must always specify both source and target locations. A single period is used to indicate the current directory in the second example. | cp myfile myfile.backup cp /tmp/testing. |

continued