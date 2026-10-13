
## Searching for info Pages

To search the info pages, use the command option -apropos followed by an equals sign, and then the search term. For example,

```
info --apropos=concatenate
```

## Special Features of Bash

As mentioned previously, we are going to focus primarily on the Bash shell in this hour because it is one of the easiest shells for new users to work with—yet it is also one of the most powerful shells available. We will look at some of the features available in Bash, including history editing and command line completion.

Bash can be installed from the FreeBSD installation CD, under the "shells" category in the packages. To run Bash, after it's installed, simply type bash at the command line. (You might have to log out and back in before the system recognizes it as a valid command.)

![](img/ba0161b65b37e94cffc801ecbacaba5e_83_0.png)

> To permanently switch your shell to Bash, use the chsh command ("change shell") and specify /usr/local/bin/bash on the Shell: line.

## Command Line History

The bash shell stores a history of the commands you have typed. If you want to repeat a command, you can move back through the history of previous commands by using the Up arrow key. You can also move forward in the list by using the Down arrow key. When you have found the command you want to run again, you can simply press Enter to re-execute the command. If you want to edit the command first, you can use the left and right arrow keys, the backspace key, and the delete key to change it. The history file in which the commands are stored is .bash_history, which is located in your home directory.

## Command Line Completion

Bash also has the capability to complete a command line for you. It can complete the name of a command as well as the name of a directory or file path. To access this feature, type the first few letters of the command or directory / file and then press the Tab key. If Bash currently doesn’t have enough information to make the command or path unambiguous (that is, there is still more than one possible match), it will complete as much of the command or path as it can until it hits the ambiguous part. At this point, it will beep, and you can enter more text and then press Tab again. This process will continue until the command line is no longer ambiguous and it can complete the entire command.

If you’ve reached an ambiguous point and you press Tab again instead of entering another character, Bash will provide you with a list of the files or commands that are potential matches for what you have typed up to this point. You can then continue typing until the command or filename is no longer ambiguous and press the Tab key again. Bash will complete the command for you. You can then check to make sure that Bash chose the correct command, as well as make any changes to the command line that you need to make, such as adding a directory or filename onto it. When you have finished editing the command line, press the Enter key and the command will be executed.

## File Permissions

Because FreeBSD is a multiuser operating system, it is important to have some way to protect unauthorized users from getting access to files that they shouldn’t have access to. FreeBSD implements file permissions to do this

File permissions are divided into three categories, and are of three types. The three categories are:

- **Owner** These permissions determine what the owner of the file can do. By default, the owner is the person who created the file.
- **Group** These permissions determine what group members can do with the file. By default, the group the file belongs to will be the primary group that the owner belongs to. (See the next hour for more information on Users and Groups.)
- **Other** These permissions determine what everyone else can do with the file. Everyone else includes anyone who is not the owner and is not a member of the group that the file belongs to.

## Displaying Permissions for a File or Directory

To display a directory listing including permissions, use the -l option to the ls command, so the command looks like ls -l. The following shows some sample lines from the output:

```
-rw-r--r-- 1 murban murban 0 Oct 29 06:28 file1
-rw-r--r-- 1 murban murban 0 Oct 29 06:28 file2
drwxr-xr-x 2 murban murban 512 Oct 29 06:28 mydir
```

The first part of each line gives the permissions. There are three types of permissions. They are:

- r Permission to read the file.
- w Permission to write to the file. This includes making changes to the file or deleting it.
- x Permission to execute the file. For normal files, this means that the file can be executed like a program. For directories, it means that the directory can be entered with the cd command.

In the directory listing, the permissions are given in the order of the previous table. If the permissions are not preset, a dash (-) will be used as a placeholder. In addition, permissions are listed in the order user, then group, then other.

In the previous listing, we can see that the first two entries are normal files, and that they have the following permissions:

- The user can read and write to the files, but can not execute them. This is indicated by the first rw-
- The group can read the file, but cannot write to the file or execute it. This is indicated by the second r--
- Other people can read the file, but cannot write to the file or execute it. This is indicated by the third r--

The third entry is a directory, as indicated by the d at the beginning of the line. In this case, we can see that the directory has the following permissions:

- The user can read the directory (list the entries with ls), write to the directory, and cd into the directory as indicated by the first rwx.
- The group can read the directory and cd into the directory, but cannot write to the directory as indicated by the second r-x.
- Other people can read the directory and cd into the directory, but cannot write to the directory as indicated by the third r-x.

So what if we want to make it so that no one can read file1 except us? This is accomplished by using the chmod command. In this case, we can simply remove all of the permissions from the group and from other. A command like the following will work:

```
chmod go-r file1
```

This command basically says to subtract read permissions (indicated by the r) from the group and from other (indicated by the g and the o). If we now do a directory listing, the entry for file1 will look like this:

```
-rw------- 1 murban murban 0 Oct 29 06:28 file1
```

What if we want to give read permissions back to the group? As you might have guessed, the command to do this would be:

```
chmod g+r file1
```

There are some other ways that you can set file permissions using the chmod command, but they are beyond the scope of this book. Please see the man page for chmod if you are interested. Man pages were discussed earlier in this hour. Also, see Hour 5 for more information on users and groups.

![](img/ba0161b65b37e94cffc801ecbacaba5e_86_0.png)

> There are a couple of potential pitfalls you need to be aware of with file permissions. The main thing you need to keep in mind is that directory permissions can override file permissions. This means, for example, that if the group has write access to a directory, anyone in that group will be able to delete any file in that directory, even if they do not have write access to the file itself. (The write privileges on the directory allow them to make changes to the directory.) Another thing to note is that if someone has execute privileges on a directory, but does not have read privileges on it, they will be able to go into the directory, but they will not be able to list the contents of the directory. However, they will still be able to read files in that directory provided that they know the name of the file.

## Process Management

As we have mentioned in previous hours, FreeBSD is a multitasking operating system. This means that you can have several processes running at the same time. Many of them might be running in the background. You can use the ps command to see a list of processes that you are currently running. If you run ps with no options, it will give you a list of only the processes that are owned by you. Several useful options to ps can be used to change what it shows you. Table 4.2 shows some of the most common and useful ones.
