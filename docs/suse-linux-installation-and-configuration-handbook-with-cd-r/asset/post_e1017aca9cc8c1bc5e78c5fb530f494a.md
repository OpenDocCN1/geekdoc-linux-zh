
- Did the patch process execute flawlessly? If not, re-patch Oracle.
- Are you using the versions described in this chapter? Other versions need different procedures. Check the Web page http://www.suse.de/en/support/oracle/ and the Oracle documentation.

## I get an error during the installation.

Do you have enough disk space? Did you set the environment variables as mentioned in this chapter? Do you have write permissions to the directories—mount points—you want your database on?

You might want to turn off the network if the CPU load is high on your machine. You might as well close all the programs that require high usage of CPU. The Oracle installation requires very high CPU usage.

## I'm finished installing, but I get an error about missing shared libraries.

This is because the shared libraries that come with Oracle are not listed in the /etc/ld.so.conf file. To add them to the shared libraries path, follow these steps:

- 1. Log in as root.
- 2. Edit the file /etc/ld.so.conf.
- 3. Add the line /opt/oracle/product/8.1.5/lib to the file, where /opt/oracle/product/8.1.5/ is the ORACLE_HOME on your system.
- 4. Run ldconfig to update the library database.

## I get the following error when I try to run sqlplus:

Message file sp1<lang>.msb not found
Error 6 initializing SQL*Plus

The environment variables are not correctly exported. Check the pre-installation procedures described in this chapter. Exporting the correct environment variables should solve this error along with any error concerning missing language files.

## Using the Shell

## In this chapter

- The Command-Line Interface 588
- Using the Shell 588
- The Bash Shell 594
- TCSH Specifics 600
- A Briefing on Midnight Commander 604
- Midnight Commander Software Requirements 604
- Configuring Midnight Commander 604

## The Command-Line Interface

Even though SuSE Linux offers you a graphical user interface, you will have to learn how to use the command line. Linux, built on the image of UNIX, has inherited all the power available for the UNIX command line. To get the most out of Linux, you should know how to use the command line. The more familiar you are with it, the more power you will be able to get out of Linux.

The command-line interface in Linux is very strong and flexible, much more so than other command lines such as MS-DOS. It will take you some time to truly master it, but once you do, your whole experience with Linux will be easy and efficient. Most of the powerful features in Linux are accessible only through the command line. So, if your whole interface to Linux is through the X Window system, you will be missing a lot.

## Using the Shell

SuSE Linux comes with a variety of shells. A shell in Linux is a command-line interpreter you use to issue commands to the operating system. When you type the ls command, you are typing it in a shell, which then executes that command by interacting with the operating system.

As mentioned previously, SuSE Linux ships with more than one type of shell. All shells work similarly, but some shells do have slight differences. However, these differences are apparent only to the experienced user. The most commonly used shells are bash (Bourne Again Shell) and csh (C Shell).

In this chapter, you will learn about the shell independent commands, the bash and csh shells, and how to write small shell scripts to automate tasks. But first, you will learn about the most common shell operations.

## Navigating Directories

One of the most basic operations a user performs is navigating through his filesystem. Navigating means moving from one directory to another, creating directories, removing directories, listing files, and so on.

To move from one directory to another using the shell, you use the cd command. This command stands for Change Directory. To change the current working directory to another directory, just type the following:

```
$ cd new directory
```

For example, if you are in /home/john and you want to change the directory to /home/john/doc, you could type the following command:

```
$ cd /home/john/doc
```

Or, if you are changing to a directory that is a child of the current directory, you could just type

```
$ cd doc
```

The shell then would assume that doc is a directory inside the one in which you are currently. To change the directory to the parent directory, you would type this command:

```
$ cd ..
```

In the previous command, the two dots (..) point to the parent directory of the directory in which you are currently. So, if you are in /home/john/doc and you run the previous command, you would end up in /home/john again. Type the command again and you would move to /home and so on.

To create a new directory, you use the mkdir command, which stands for Make Directory. For example, to create a directory called files in /home/john, you could type

```
$ mkdir /home/john/files
```

Again, if you are currently in /home/john, you could just type the following command:

```
$ mkdir files
```

The previous command causes the shell to assume you want to create this directory right here. If you want to create a whole family of directories in one step, you can use the -p option. For example, if you want to create the directory /home/john/files/pics, the command

```
$ mkdir -p /home/john/files/pics
```

creates the directory pics and all its parent directories if they don't already exist. This is easier than first creating /home/john/files and then creating /home/john/files/pics.

To remove a directory, you can use the rmdir command, which stands for Remove Directory. For example, to remove the directory called pics, you could type the following:

```
$ rmdir /home/john/files/pics
```

The directory must be empty, though. So, you should use the rm command to delete all the files in it first:

```
$ rm -r /home/john/files/pics
```

shows you a long listing of all the files. The long listing will show you the size of each file, the date each was last modified, and so on.

The following command includes all the hidden files in the directory listing:

```
$ ls -a
```

## Copying, Moving, and Renaming Files

Manipulating files and directories is a frequently performed task for most users. You will surely find yourself needing to copy a file here, move a file there, rename a file, and so on. Most of these operations are easily accessible from graphical desktop environments such as KDE or GNOME. But, knowing how to perform them using the shell is definitely beneficial because you will not need to switch to a graphical desktop environment to copy some files.

To copy a file using the shell, you use the cp command. In its simplest form, if you want to copy a file from one place to another, you type the following:

```
$ cp filename destination
```

For example, to copy the file mail.txt to /tmp, you use the following command:

```
$ cp mail.txt /tmp
```

You also can use wildcards; for example,

```
$ cp *.doc /tmp
```

copies all files that end with the extension .doc to /tmp. You can copy entire directories using the -R option:

```
$ cp -R /usr/ /mnt/backup
```

The previous command copies all the contents of /usr recursively to /mnt/backup.

To move files from one place to another, you use the mv command. This command is quite similar to the cp command. For example, to move a file from one place to another, you would use this command:

```
$ mv mail.txt /tmp
```

This moves the file called mail.txt to /tmp. The original file will no longer exist where it was; it will be moved to /tmp. You can consider this a copy operation followed by a delete operation on the file at its original location.

You can move entire directories using the mv command, for example:

```
$ mv documents/ /tmp/backup/
```

This moves the directory called documents/ to /tmp/backup. Note that you cannot move directories across filesystems. The mv command also is used to rename files. For example, to rename the file called mail.txt to oldmail.txt, you would type the following:

```
$ mv mail.txt oldmail.txt
```
