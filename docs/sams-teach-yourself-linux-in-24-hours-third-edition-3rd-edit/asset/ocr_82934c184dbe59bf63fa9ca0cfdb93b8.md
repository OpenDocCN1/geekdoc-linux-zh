In this hour, you will

+   - Work with files by changing between directories and displaying the list of files contained in a directory
+   - Add and delete directories and files in your user account
+   - Create files and view the file properties
+   - Copy and rename files

# Exploring the Home Directory

In Hour 4, “Understanding the Linux Operating System,” you were introduced to the basic structure of the filesystem. You saw how files fit into directories, and how directories fit within other directories. When users are assigned accounts on the system, they are also allocated space within the /home directory in which to store their personal files. If a user has the login name of rusty, that user’s personal files are stored in /home/rusty. This is known as the home directory and is the directory in which the user is working after logging in to his account. From this directory, the user can create subdirectories in which to organize files, create new files, modify these files, and delete unneeded files. Only the user, those authorized by the user, and the root account, may access files in the user’s home directory.

When you first log in to your user account, the shell prompt looks something like this (that is, if your username is rusty):

```
[rusty@localhost rusty]$
```

Cool, but where does that leave you in the filesystem? Type pwd and press Enter. The response appears on the following line on the screen and looks like this for the user named rusty:

```
/home/rusty
```

Notice that the shell prompt appears on the next line. It’s waiting for you to give it another command. That’s good, because this is a good time to explore your home directory.