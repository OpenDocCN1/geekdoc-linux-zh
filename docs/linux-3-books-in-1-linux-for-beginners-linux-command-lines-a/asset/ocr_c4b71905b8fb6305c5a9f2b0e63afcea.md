was typed by you.

```

[student@desktop ~]$ history
1 clear
2 who
3 pwd
[student@desktop ~]$ !3
/home/student

```

You can see that !3 expanded the entire command for pwd and even showed the output for the user’s present working directory.

You can use the keyboard arrow keys to navigate through the output of the history command. The up arrow key takes you to the commands on top, while the down arrow key takes you to the commands below. The left and right arrow keys will help you edit the command that you are on at present.

# # File Management Through the Command Line

This section will go through some important commands that will help you manage files and directories on Linux. You will learn commands that will let you create, delete, copy, move, and organize files and directories.

# ## Linux File System Hierarchy

To understand the Linux file system properly, you need to understand the Linux file system hierarchy first. The Linux file system hierarchy visually looks like an inverted tree with the root at the top and then branching downwards to form other parts.

The root directory is represented as / and is located at the top of the file system hierarchy. The / character is also used to represent file paths in Linux. For instance, **var** is a subdirectory under the root directory and is represented as /var. Similarly, there is a subdirectory called **log** under the var directory, and its path is represented as /var/log.

The root directory has a particular set of subdirectories under it that store