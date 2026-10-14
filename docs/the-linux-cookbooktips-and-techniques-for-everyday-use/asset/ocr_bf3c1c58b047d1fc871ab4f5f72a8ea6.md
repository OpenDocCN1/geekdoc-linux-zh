# W(1) Linux Programmer’s Manual W(1)

# NAME

w - Show who is logged on and what they are doing.

# SYNOPSIS

```
w = [husfV] [user]
```

# DESCRIPTION

w displays information about the users currently on the machine, and their processes. The header shows, in this order, the current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes.

The following entries are displayed for each user: login name, the tty name, the remote host, login time, idle time, JCPU, PCPU, and the command line of their current process.

The JCPU time is the time used by all processes attached

Manual page W(1) line 1

Use the up and down arrow keys to move through the text. Press Q to stop viewing the manual page and exit man. Since man uses less to display the text, you can use any of the less keyboard commands to peruse the manual page (see section Perusing Text).

Despite its name, a manual page does not always contain the complete documentation to a program, but it’s more like a quick reference. It usually gives a short description of the program, and lists the options and arguments it takes; some manual pages also include an example or a list of related commands. (Sometimes, commands have very complete, extensive manual pages, but more often, their complete documentation is found either in other help files that come with it or in its Info documentation; these are subjects of the following two recipes.)

To prepare a man page for printing, see Preparing a Man Page for Printing.

+   [ < ] [ > ] [ << ] [ Up ] [ >> ] [Top] [Contents] [Index] [ ? ]

# 3.8.5 Using the GNU Info System

The GNU Info System is an online hypertext reference system for documentation prepared in the Info format. This documentation tends to be more complete than a typical man page, and often, the Info documentation for a given software package will be an entire book or manual. All of the manuals published by the Free Software Foundation are released in Info format; these manuals contain the same text (sans illustrations) as the paper manuals that you can purchase directly from the Free Software Foundation.

There are different ways to peruse the Info documentation: you can use the standalone info tool, read Info files in the Emacs editor (see section Emacs), or use one of the other tools designed for this purpose. Additionally, tools exist for converting Info documentation to HTML that you can read in a Web browser (see section Browsing Files).

To read the Info manual for a tool or application with the info tool, give its name as an argument. With no