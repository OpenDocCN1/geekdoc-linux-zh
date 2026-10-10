For this task, you should log in as an ordinary user. In fact, it’s good practice to *always* log in as an ordinary user. You can subsequently acquire superuser privileges from your ordinary user account if you need such access (described shortly in “Obtaining Superuser Privileges”).

Logging in as an ordinary user and then obtaining superuser privileges is better than logging in directly as *root* because this two-step process leaves a trace in the system log file of who acquired *root* privileges. On systems with multiple administrators, this can make it easier to track down who caused problems if an administrator makes a mistake.

![](bbox=[0.15, 0.26, 0.28, 0.33])

> The Linux system administration account is conventionally called *root*, but it’s possible to configure Linux with aliases for this name. Under any name, this account is often referred to as the *superuser* account.

# Verifying the Presence of a File

To verify that a file is present, use the `ls` command. This command’s name stands for *list*; it shows a list of files that match a file specification you provide. (Task 1.2 describes file specifications in more detail.) For now, check for the presence of the *what1s* file, which is located in the `/usr/bin` directory:

```
$ ls /usr/bin/what1s
/usr/bin/what1s
```

Used without any extra parameters, `ls` displays the names of all the matching files. Because this example provides the complete name of a single file, only that filename is displayed, on the line immediately following the command’s line.

If you type the name of a directory, `ls` displays the names of all the files in that directory. Try this with the `/usr/bin` directory now—but be prepared for copious output! The `/usr/bin` directory holds the program files associated with many (but not all) Linux commands.

Like many Linux commands, `ls` accepts options that modify its actions. One of the most important is `-1` (that’s a lowercase *L*, not a number *1*), which generates a “long” listing:

```
$ ls -l /usr/bin/what1s
-rwxr-xr-x  1 root root 2409 Nov 19  2004 /usr/bin/what1s
```

I describe what this output means in more detail in Task 1.2.

# Examining the File

Now that you know the command file is present, you can examine it. Three commands are very handy for examining text files:

+   * **cat** This command’s name is short for *concatenate*, and it’s used to merge two or more files together. If it’s passed just one filename, though, it copies the file to the screen. This can be a good way to look at a short text file. Try it on the *what1s* file by typing `cat /usr/bin/`