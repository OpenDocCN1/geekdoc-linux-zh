group permissions of the file or directory are used to assign access (or deny it in this case); the rights assigned to other users are never considered.

In the next section, you learn about several other commands for securely managing user access to Linux systems and for communicating with users who are logged in.

# User Security Issues

File permissions are a critical part of user security. They control which files and directories a regular user can access, and determine what the users can do with those files and directories (execute them, create files in a directory, and so forth). This section describes some additional communications and user security mechanisms in Linux.

# Communicating with Users

Two methods of communicating with users were popular before graphical desktops became the standard for Linux users. Knowing about these may still be useful to you on occasion.

On a system with many users, you often need to communicate with all the users on the system regarding planned system maintenance or some other aspect of how people are using the computer system. In Linux, each time a user logs in, the contents of the file /etc/motd are displayed just before the shell is started. This file, which is the "message of the day," is sometimes used for fun sayings or quotes, or (in a more serious environment), for news of upcoming maintenance, requirements about changing passwords or backing up files, or other system administrative functions that users need to be informed about. The /etc/motd file does not appear, however, unless the user opens a command line or logs in at a text-mode console.

A second method of communicating with users is the wall command (for write all). Use this command when you need to communicate an immediate message to all users who are logged in to the system. This command displays a broadcast message on the command line for all users who are working in text mode or have an open terminal window. Depending on the type of day you are having, you can use this for messages such as "Free bagels in the breakroom" or "Emergency system shutdown in 3 minutes—save your work!!" The format is simple. Here is an example of what you would enter as root:

```
# wall Meet in the conference room in 5 minutes for an
announcement from Evelyn
```

Using /etc/motd and the wall command are alternatives to using an e-mail addressed to each user. Each method has advantages and disadvantages.

In addition to communicating with users, you can learn about what users are doing with the fuser command. Recall that when you have file systems mounted, you cannot unmount a file system if any user is working in that file system. For example, if a user has a file from that file system open, or even has a directory in that file system as their current working directory,