# Using the Manual Pages

Linux has a set of manual pages that explain most of the commands and programming API available. You can access this manual using the man command. For example, to find the manual page for the ls command, type the following:

```
$man ls
```

Manual pages are in sections. The following are the available sections:

+   - Section 1: User Commands
+   - Section 2: System Calls
+   - Section 3: Subroutines
+   - Section 4: Devices
+   - Section 5: File Formats
+   - Section 6: Games
+   - Section 7: Miscellaneous
+   - Section 8: System Administration
+   - Section n: Tcl/Tk

To access a section, just type its number after the man command. For example, the following searches section 1 for the command you enter after the 1:

```
$ man 1 command
```

You can use the -k option if you want man to search all the sections for the command you want.

# Changing the Priority of Your Processes

Processes in Linux get CPU time according to their priority. The higher the priority, the more CPU time the process will get. To change the priority of a process, use the nice command. Priorities are a numerical value that ranges from -20-19, with 0 as the default. The lowest priority is 19, whereas the highest priority is -20.

To change the priority of a process, type the following:

```
$ nice 10 pid of process
```

You should note that a normal user cannot change the priority of a process to a number below 0, only root can do that. You can only change the priority of a process you own.

# Viewing Files in Pieces

You can use the head command to view the top 10 lines of a file. You can do the opposite using the tail command, which will show you the last 10 lines in a file. You can use the -f option in tail to cause it to continuously list the last 10 lines of a file as it grows in size.