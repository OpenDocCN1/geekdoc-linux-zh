
# WHERE TO FIND DOCUMENTATION 137

![](img/45ff4cd21497435daa35084a84b95d07_187_0.png)

# Ubuntu Help Center

# Topics

Welcome to the Ubuntu Help Center

To find help, insert a keyword in the search bar

New to Ubuntu?

# Common Questions

Adding, Removing and Updating Applications

- Connecting to the internet
- Enabling visual effects
- Playing music
- Importing photos
- Keeping your computer updated

Files, Folders and Documents

# Can't find the answer?

Customizing Your Computer

The Ubuntu community provides extensive free support

Internet and Networks

Canonical, partners and approved companies provide commercial technical support

Music, Video and Photos

# How to Contribute

Assistive Tools

Ubuntu has an open and vibrant community of contributors. Find out how to contribute

Keeping Your Computer Safe

Figure 4-28 The Ubuntu Help Center

To find out about a utility, give the command man, followed by the name of the utility. Figure 4-29 shows man displaying information about itself; the user entered a man command.

![](img/45ff4cd21497435daa35084a84b95d07_187_1.png)

Figure 4-29 The man utility displaying information about itself

# 138 CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

less (pager) The utility automatically sends its output through a pager—usually less (page 162), which displays one screen at a time. When you access a manual at the bottom this manner, less displays a prompt [e.g., Manual page man(1) line 1] at the bottom of the screen after it displays each screen of text and waits for you to request another screen of text by pressing the SPACE bar. You can also use the PAGE UP, PAGE DOWN, UP ARROW, and DOWN ARROW keys to navigate the text. Pressing h (help) displays a list of less commands. Pressing q (quit) stops less and causes the shell to display a prompt. You can search for topics covered by man pages using the apropos utility (page 139).

Manual sections Based on the FHS (Filesystem Hierarchy Standard; page 213), the Linux system manual and the man pages are divided into ten sections, where each section describes ruled tools:

1. User Commands
2. System Calls
3. Subroutines
4. Devices
5. File Formats
6. Games
7. Miscellaneous
8. System Administration
9. Kernel
10. New

This layout closely mimics the way the set of UNIX manuals has always been divided. Unless you specify a manual section, man displays the earliest occurrence in the manual of the word you specify on the command line. Most users find the information that they need in sections 1, 6, and 7; programmers and system administrators frequently need to consult the other sections.

In some cases the manual contains entries for different tools with the same name. For example, the following command displays the man page for the passwd utility from section 1 of the system manual:

```bash
$ passwd
```

To see the man page for the passwd file from section 5, enter this command:

```bash
$ man 5 passwd
```

The preceding command instructs man to look only in section 5 for the man page. In documentation you may see this man page referred to as passwd(5). The -a option (see the adjacent tip) to view all man pages for a given subject (press RETURN to display each subsequent man page). For example, give the command man -a to view all man pages for passwd.

# Options

tip An option modifies the way a utility or command works. Options are usually specified as one or more letters that are preceded by one or two hyphens. An option typically appears following the name of the utility you are calling and a SPACE. Other arguments (page 1135) to the command follow the option and a SPACE. For more information refer to "Options" on page 239.

# apropos: SEARCHES FOR A KEYWORD

When you do not know the name of the command required to carry out a particular task, you can use apropos with a keyword to search for it. This searches for the keyword in the short description list of all man pages and displays that contain a match. The man utility, when called with the -k (keyword) option, provides the same output as apropos.

The database apropos used, whatis, is not available on Ubuntu systems when they are first installed, but is built automatically by cron (page 605) using mandb. If apropos does not produce any output, the command mandb.

The following example shows the output of apropos when you call it with the who keyword. The output includes the name of each command, the section of the man page that contains it, and the brief description from the man page. This list includes the utility you need (who) and identifies other, related tools you might find:

```text
$ who
at.allow (5) - determine who can submit jobs via at or batch
at.deny (5) - determine who can submit jobs via at or batch
from (1) - print names of those who have sent mail
w (1) - show who is logged on and what they are doing.
w.proprops (1) - show who is logged on and what they are doing.
who (1) - show who is logged on
whoami (1) - print effective userid
```

whatis The utility is similar to apropos but finds only complete word matches for the name of the utility:

- whatis - show who is logged on

# info: DISPLAYS INFORMATION ABOUT UTILITIES

The textual info utility is a menu-based system distributed with Ubuntu. It includes a tutorial on many utilities. Figure 4-30 shows the screen that info displays.

When a man page displays abbreviated information on a utility that is covered by info, the man page refers to info. 

Because the information on this screen is drawn from an editable file, the page may differ from the screens shown in this section. You can press any of the following keys while the initial screen is displayed:

- h to go through an interactive tutorial on info
- ? to list commands
- SPACE to scroll through the menu of items for which information is available
- m followed by the name of the menu you want to display or a SPACE to display a list of menus
- q or CONTROL-C to quit

The notation info uses to describe keyboard keys may not be familiar to you. The notation C-h is same as CONTROL-H. Similarly, M-x means hold the META or ALT key and press x. (On some systems you need to press ESCAPE and then duplicate the function of META-X).

After giving the command coreutils, press the SPACE bar a few times to scroll through the display. Type sleep RETURN search for the string sleep. When you type /, the cursor moves to the bottom line of the window and displays Search for string [string], where string is the last string you searched. Press RETURN to search for string or enter the string you want to search. Typing displays sleep on that line, and pressing RETURN displays the next occurrence of sleep.

# 140 CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

```text
$ coreutils --help
***********************************
Welcome to coreutils version 4.13. Type H for help, M for menu item.
File: coreutils.info, Node: Top, Next: Introduction, Up: dir
coreutils

Menu:
Introduction: Caveats, overview, and others.
Common options.
```

Figure 4-30 The initial screen displayed by the command coreutils
