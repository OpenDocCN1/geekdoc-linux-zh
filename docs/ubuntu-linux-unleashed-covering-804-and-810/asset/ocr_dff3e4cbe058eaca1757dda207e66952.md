the terminal while remaining in Gnome. This time, the terminal appears as black text on a white background. Accessing the terminal this way, or by using the Ctrl + Alt + F1 method makes no difference because you are interacting directly with the terminal itself.

# Navigating Through the File System

Use the cd command to navigate through the Ubuntu file system. This command is generally used with a specific directory location or pathname, like this:

```
$ cd /etc/apt/
```

Under Ubuntu, the cd command can also be used with several shortcuts. For example, to quickly move up to the parent (higher-level) directory, use the cd command like this:

```
$ cd ..
```

To return to one's home directory from anywhere in the Linux file system, use the cd command like this:

```
$ cd
```

You can also use the $HOME shell environment variable to accomplish the same thing. Type this command and press Enter to return to your home directory:

```
$ cd $HOME
```

You can accomplish the same thing by using the tilde (~) like this:

```
$ cd ~
```

Don't forget the pwd command to remind you where you are within the file system!

Another important command to use is the ls command, which lists the contents of the current directory. It's commonly used by itself, but a number of options (or switches) available for ls give you more information. For instance, the following command returns a listing of all the files and directories within the current directory, including any hidden files (denoted by a . prefix) as well as a full listing, so it will include details such as the permissions, owner and group, size and last modified time and date:

```
$ ls -al
```

You can also issue the command

```
$ ls -R
```

which scans and lists all the contents of the sub-directories of the current directory. This might be a lot of information, so you may want to redirect the output to a text file so you can browse through it at your leisure by using the following:

```
$ ls -alR > listing.txt
```