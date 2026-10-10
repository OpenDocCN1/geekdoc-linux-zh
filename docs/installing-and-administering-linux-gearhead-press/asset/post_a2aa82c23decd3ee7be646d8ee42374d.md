
- `-i, -u, -idle`
    add user idle time as HOURS:MINUTES, or old
- `-l, -lookup`
    attempt to canonicalize hostnames via DNS
- `-m`
    only hostname and user associated with stdin
- `-g, -count`
    all login names and number of users logged on
- (etc.)

The coding in the Synopsis section uses these typographical conventions.

Optional fields appear in square brackets, [ and ]. They mean that you need not enter an option or argument. Mandatory fields, if there were any, would appear in curly brackets: { and }. If there were mandatory fields, then you would have to enter a value for the respective option or argument after the command name. When you see a pipe character ( | ) separating two mandatory options or arguments, then you would have to enter one or the other with the command. In the case of who, though, the arguments—although separated by a pipe—are optional. So you would not have to supply anything unless you chose to do so.

You might have noticed the FILE option in the who man page. When users are logged in, a record of their login is kept in the file /var/run/utmp. By default, the who command looks there for the information. If the system administrator has configured the system to use another file to record login information, then you would have to specify that filename after the who command.

## info Pages

The info pages use the same database as man but present the information in a different format. Some say info is more powerful because it enables you to examine information in more bite-sized chunks and shows the relationships between the information you have searched for and other related information.

Another important feature of info, especially for new users, is that it presents its own instructions on the first screen and also enables you to enter a primer immediately after you invoke info. This hand-holding approach greatly enhances the likelihood of a successful search.

The syntax could not be simpler:

```
$ info<Enter>
```

After invoking the command, the first ASCII character-based *info* screen appears and declares that you are at the top of the *info* directory tree. Basic instructions follow as well as the opportunity to start the *info* primer.

If you do not require the primer, press the Tab key or the up and down arrow keys to move among the many available user commands, system calls, subroutines, devices, file formats, games, system administration functions, and more. Example 3.5 lists the basic categories but not all the functions you can access from this screen. When you have selected a category, press the Enter key. You are then presented with a screen containing information about your selection.

After a user exits from *info*, however, there is no command similar to *fg* (as we used with *man*) to return the user to the point where they left *info*. They have to re-enter at the beginning and go through the whole procedure again.

Users can also invoke *info* from *xterm* windows, and additional *info* or *man*-like programs can be invoked from the X Window system desktop. The names and types of these programs vary with each X window manager. From KDE, for example, you can invoke KDE Help. KDE Help enables you to navigate through hyperlinks with a mouse as opposed to the keyboard navigation we used to get through the ASCII-oriented *info* pages. See Chapter 14, “The Linux X Window System,” for more information about the X Window System and X window managers.

> **NOTE** Check the *man* pages and other information sources for the options and arguments for all the commands mentioned in this chapter.

### Example 3.5 Obtaining Command Information with *info*

Let’s say that Sancho wants to compare the who information provided by *man* to that provided by *info*. To invoke the *info* command, he types:

```
$ info<Enter>
```

Linux responds with the *info* directory tree, whose approximately 250 lines are structured like the following:

```
File:dir          Node:top    This is the top of the INFO tree

"Basic Instructions"

*Menu:

Texinfo documentation system
Miscellaneous (i.e., list of common commands)
Programming Languages
GNU Gettext Utilities
GNU Packages
Libraries
Individual Utilities
Net Utilities
World Wide Web
Printing Tools
C library code
Programming
GNU Emacs
GNU Admin
Programming & development tools
GNU libraries
Indent Code Formatter
GNU programming tools
```

We know that Sancho wants to know something about the who command. With the Tab key or the up or down arrow keys, he moves the cursor to who under Miscellaneous and selects who by pressing Enter. Linux then jumps, or hyperlinks, to the who information:

```
'who': Print who is currently logged in
=================================================
'who' prints information about users who are currently logged on.
"Synopsis"
"Explanation"
"Options"
(etc.)
```

Sancho can navigate up and down through the information. He can press the following:

- The space bar to navigate down the file one screen at a time
- h to display help
- / followed by a string and Enter to search for the string in the text
- n to move to the next related topic or function (if any)
- p to move to a previous related topic or function
- d to return to the first screen (that is, back to the top of the **info** directory)
- q to exit **info**

## The usage Utility

The **usage** utility can prove invaluable. It is based on the same database used by **man** and **info**. You invoke this facility in two ways. First, let’s invoke it by requesting command **usage** help. The syntax is as follows:

```
$ **commandname** -help<Enter>
```

The second way to invoke **usage** is basically accidental. If you enter a command incorrectly, Linux responds with information on what is wrong with what you did, and then (by using **usage**) it tells you how to correct the command entry.

Example 3.6 illustrates the two ways **usage** gets invoked.

### Example 3.6 Invoking the usage Utility

Sancho has always been something of a *sneakernet* proponent—that is, he still occasionally uses floppy disks. Naturally, he wants to know how to use the floppy disk drive on his Rueful Figures, Inc. system. Preston, the system administrator, has told him that he has to become familiar with the **mount** command. Sancho seems to recall a -d option that he could use with **mount**. Here, he will check by invoking **usage**. First, he deliberately requests information for the **mount** command:

```
$ **mount** -help<Enter>
Usage: **mount** -v
: print version
**mount** -h
: print this help
**mount**
: list mounted **filesystems**
**mount** -l
: idem, including volume labels
So far the informational part. Next the mounting.
The command is ‘**mount** [ -t *fstype*] something somewhere’.
Details found in /etc/fstab may be omitted.
(/etc.)
```

Sancho does not see a -d option, but he thinks there might be an oversight. So, he will take a chance and deliberately enter the **mount** command with a -d option to see how Linux responds:

```
$ mount -d /dev/Fd0<Enter>
```

Here is Linux's response:

```
mount: invalid option -d
Usage:    mount -V        : print version
          mount -h        : print this help
          mount           : list mounted filesystems
          mount -l        : idem, including volume labels
So far the informational part. Next the mounting.
The command is `mount [ -t fstype] something somewhere`.
Details found in /etc/fstab may be omitted.
(etc.)
```

Convinced that there is no -d option after all, Sancho decides to pursue other mount options. Meanwhile, we will discuss the mount command in Chapter 4, “Files and Directories in Linux.”

## Viewing the Date: date and cal Commands

Now that we know 1) something about command syntax and 2) where to go for help with our commands; let's look at some common commands we use in everyday administration.

Freston's responsibilities as system administrator include setting the date globally for the Ruel Figure, Inc. network. Once he has done that, the users can then display the date on their own systems by entering the date command.

When you use the date command to display the date, you can customize it in several ways—but by default, it requires no options. (For more information on setting the date, consult the man pages for the date command.) The syntax is simply

```
$ date<Enter>
```

Linux responds with a time based on a 24-hour clock (for example, 1 P.M. is indicated as 13:00:00), followed by the date and the time zone (for example, CST for Central Standard Time).

The syntax for the cal (calendar) command is as follows:
