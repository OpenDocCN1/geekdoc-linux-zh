# Listing Directories and Files with ls

![](bbox=[0.07, 0.08, 0.42, 0.68])

Your Unix system is made up of directories and files that store a variety of information, including setup information, configuration settings, programs, and options, as well as other files and directories. You might think of your Unix system as being a tree (tree roots, actually), with subdirectories stemming from higher-level directories. As shown in Figure 1.6, all of these files and directories reside within the root directory, which contains everything in the system.

Using the ls command, you can find out exactly what's in your Unix system and thereby find out what's available to you. You can list the files and directories of a directory that you're currently in or a directory that you specify.

# To list the files and directories of the directory you're in:

+   - ls

At the shell prompt, type ls to list the files and directories in the current directory, which in this case is our home directory (Code Listing 1.2).

Figure 1.6 All files and directories are nested within the root directory, which serves to contain everything in the system.

```
[jdoe@frazZ jdoe]$ ls
limerick mail/ Project/ public_html/
* testfile testlink@ tmp/
[jdoe@frazZ jdoe]$
```

Code Listing 1.2 Use ls by itself to list the files and directories of the directory you're in.