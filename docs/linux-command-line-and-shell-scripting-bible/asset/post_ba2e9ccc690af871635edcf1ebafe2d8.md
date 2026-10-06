
# Part I The Linux Command Line

# FIGURE 3-2

The Linux file structure

![](img/adcbcf1053b52dbf22f3aa187738232f_97_0.png)

The Linux filesystem structure has evolved from the Unix file structure. Nowadays the file structure has been somewhat convoluted over the years by different flavors of Unix. Nowadays it seems that no two Unix or Linux systems follow the same filesystem structure. However, there are a few common directory names that are used for common functions. Table 3-4 lists some of the more common Linux virtual directory names.

When you start a new shell prompt your session starts in your home directory, which is a unique directory assigned to your user account. When you create a user account, the system normally assigns a unique directory for the account (see Chapter 6).

In the Windows world, you're probably used to moving around the directory structure using a graphical interface. To move around the virtual directory from a CLI prompt, you'll need to learn to use the cd command.

## Traversing directories

The change directory command (cd) is what you'll use to move your shell session to another directory in the Linux filesystem. The format of the cd command is pretty simplistic:

```
cd destination
```

The cd command may take a single parameter, destination, which specifies the directory name you want to go to. If you don't specify a destination on the cd command, it will take you to your home directory.

The destination parameter, though, can be expressed using two different methods:

- * An absolute filepath
- A relative filepath

## Common Linux Directory Names

| Directory | Usage |
| --- | --- |
| / | The root of the virtual directory. Normally, no files are placed here. |
| /bin | The binary directory, where many GNU user-level utilities are stored. |
| /boot | The boot directory, where boot files are stored. |
| /dev | The device directory, where Linux creates device nodes. |
| /etc | The system configuration files directory. |
| /home | The home directory, where Linux creates user directories. |
| /lib | The library directory, where system and application library files are stored. |
| /media | The media directory, a common place for mount points used for removable media. |
| /mnt | The mount directory, another common place for mount points used for removable media. |
| /opt | The optional directory, often used to store optional software packages. |
| /root | The home directory. |
| /sbin | The system binary directory, where many GNU admin-level utilities are stored. |
| /tmp | The temporary directory, where temporary work files can be created and destroyed. |
| /usr | The user-installed software directory. |
| /var | The variable directory, for files that change frequently, such as log files. |

The following sections describe the differences between these two methods.

## Absolute filepaths

You can reference a directory name within the virtual directory using an absolute filepath. The absolute filepath defines exactly where the directory is in the virtual directory structure, starting at the root of the virtual directory. Sort like a full name for a directory.

Thus, to reference the apache directory, that's contained within the lib directory, which in turn is contained within the usr directory, you would use the absolute filepath:

```
/usr/lib/apache
```

With the absolute filepath there's no doubt as to exactly you want to go. To move to a specific location in the filesystem using the absolute filepath, you just specify the full pathname in the cd command:

```
rich@1[~]$cd /etc
rich@1[etc]$
```

# The Linux Command Line

The prompt shows that the new directory for the shell after the cd command is now /etc.
You can move to any level within the entire Linux virtual directory structure using the absolute filepath:

```
rich@~$ cd /usr/lib/apache
rich@[apache]$
```

However, if you're just working within your own home directory structure, often using absolute filepaths can get tedious. For example, if you're already in the directory /home/rich, it seems somewhat cumbersome to have to type the command:

```
cd /home/rich/Documents
```

just to get to your Documents directory. Fortunately, there's a simpler solution.

## Relative filepaths

Relative filepaths allow you to specify a destination filepath relative to your current location, without having to start at the root. A relative filepath doesn't start with a forward slash, indicating the root directory.

Instead, a relative filepath starts with either a directory name (if you're traversing to a directory under your current directory), or a special character indicating a relative location to your current directory location. The two special characters used for this are:

- The dot (.) to represent the current directory
- The double dot (..) to represent the parent directory

The double dot character is extremely handy when trying to traverse a directory hierarchy. For example, if you are in the Documents directory under your home directory and need to go to your Desktop directory, also under your home directory, you can go to:

```
rich@[Documents]$ cd ../Desktop
rich@[Desktop]$
```

The double dot character takes you up one level to your home directory, then the /Desktop portion takes you back down into the Desktop directory. You can use as many double dot characters as necessary to move around. For example, if you are in your home directory (/home/rich) and want to go to the /etc directory, could type:

```
rich@~$ cd ../../etc
rich@[etc]$
```

Of course, in a case like this, you actually have to use the relative filepath rather than just typing the filepath, /etc!

## File and directory Listing

The most basic feature of the shell is the ability to see what are available on the system. The list command (ls) is the tool that does that. This section describes the ls command, and all of the options available to format the information it can provide.

### Basic listing

The ls command at its most basic form displays the files and directories located in your current directory:

```
$ ls
rich Desktop Music Public store.zip
backup Documents myprog store.sql Videos
```

Notice that the ls command produces the listing in alphabetical order (in columns rather than rows). If you're using a terminal emulator that supports color, the ls command may also show different types of entries in different colors. The LS_COLORS environment variable controls this feature. Linux distributions set this environment variable depending on the capabilities of the terminal emulator.

If you don't have a terminal emulator, you can use the -F parameter with the ls command to easily distinguish files from directories. Using the -F parameter produces the following output:

```
$ ls -F
rich/ Documents/ Music/ Public/ store.zip Videos/
...
```

The -F parameter flags the directories with a forward slash, to help identify them in the listing. Similarly, it flags executable files (like the myprog above) with an asterisk, to help you find the files that can be run on the system.

The basic ls command can be somewhat misleading. It shows files and directories contained in the current directory, but not necessarily all of them. Linux often uses hidden files to store configuration information. In Linux, hidden files are files with filenames that start with a period. These files do not appear in the default ls listing (thus they are called hidden).

To display hidden files along with normal files and directories, use the -a parameter. Figure 3-3 shows an example of using the -a parameter with the ls command.

Wow, that's quite a difference. In a home directory for a user who has logged into the system with a graphical desktop, you'll see lots of hidden configuration files. This particular example is from a user logged into a GNOME desktop session. Also notice that there are three that
