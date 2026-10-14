
```
code=$HOME/projects/src/spew
```

and then, regardless of what directory you are in, you can issue

```
cd $code
```

to pop over quickly to the directory containing the source code for that way-cool spew program you're developing. (The cd command means "change directory.")

A variable assignment like this will work just fine, but its scope (visibility) is limited to the current shell. If you launch a program or enter another shell, that child task will not know about your environment variables unless you export them first.

Unless you know for sure that an environment variable will have meaning only in the current shell, it's a good idea to always use export when creating variables to ensure they will be global in scope—for example,

```
export PS1="\u \$ "
export code=$HOME/projects/src/spew
```

And be sure to add these commands to your .bashrc file so you won't have to retype them each time you log in.

## How to Get Help

Need help figuring out what a command is supposed to do? In an operating system with strange-sounding commands like awk, grep, and sed, it's not surprising. The man command (short for manual) is a source of online help for most Linux commands. For example, you can enter

```
man grep
```

to learn all the secrets of the very useful grep command. (For a summary of the most-used Linux commands, see Chapter 6, "Important Linux Commands.")

If man claims no knowledge of the command in which you're interested, try help instead. This command will list all the built-in bash commands with a brief syntax summary.

Another help format called info is more powerful, since it provides hypertext links to make reading large documents much easier, but not all documentation is available in info format. There are some very complete info documents on various aspects of Red Hat (especially the portions from the GNU project).
To try it out, use the info command without any arguments. It will present you with a list of available documentation. Press h to read the help for first-time users, or use the TAB key to move the cursor to a topic link and then press ENTER to follow the link. Pressing p returns you to the previous page, n moves you to the next page, and u goes up one level of documentation. To exit info, press q.

## THE GNOME HELP BROWSER

If you're running X Windows with the GNOME interface (the default when you install Red Hat Linux), you can access the man and info pages much more easily. Just click on the taskbar button with the big question mark (see Figure 4-4), and you'll launch the GNOME Help Browser (Figure 4-5). From there, you can browse a catalog of man or info pages, along with special help files for the GNOME interface.

![](img/3137cdda7122042e86dbeafe9840d4ed_143_0.png)

Figure 4-4: The GNOME taskbar with the ? button

![](img/3137cdda7122042e86dbeafe9840d4ed_143_1.png)

Figure 4-5: The GNOME Help Browser

## THE LINUX FILE SYSTEM

- What Is a Linux File? 116
- Directories 118
- Listing Files 122
- Displaying Files 125
- Copying Files 127
- Renaming Files 127
- Creating Files 128
- Deleting Files 129
- Creating Directories 129
- Deleting Directories 130
- Using Wildcards 130
- Don't Try This at Home 131
- Controlling Access to Your Files with Permissions and Owners 132

When you installed Linux, one of the first things you did was create a file system. In the process, you carved out a chunk of hard disk and formatted it so that Linux could use it. You also created a hierarchical (treelike) structure for storing files, to impose some order on the file system to help both you and the Linux system find needed files.

In this chapter, you’ll learn how to work with files and directories in a Linux system. You’ll understand how the file system is structured to separate system data from personal data and how to navigate through it. We’ll cover three ways to manipulate your files: using the command line, the Midnight Commander, and the graphical File Manager.

When you’re done, you’ll be creating, deleting, copying, renaming, listing, linking, and protecting your files like a pro. You’ll also learn the Nine Deadly Keystrokes—or how to wipe out the entire file system without really trying. (But don’t worry; this command can affect you only if you’re logged in as root.)

Log in as hermie and try the examples in this chapter as you read through it. You’ll find that the Linux file system is a lot like DOS, only more robust and flexible.

### What Is a Linux File?

We’ve created a structured file system and filled it with a whole bunch of files—without knowing what Linux files are. Here’s what files are in the Linux world and how they are named.

### Types of Files

In most operating systems, a file is simply a blob of data stored on disk with a unique name. A file could be a list of names and numbers, a cheesecake recipe, or an executable program. But under Linux, everything is a file. In addition to data and executable files, Linux treats directories and even the various components of your computer as files.

This means there are files that represent your keyboard, console, printer, CD-ROM, and even your system’s RAM. These special files are called devices, and they are found in the /dev directory (see Figure 5-1). (If you look in this directory later, you’ll see files such as /dev/fdo
