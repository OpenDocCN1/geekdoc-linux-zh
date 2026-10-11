
applications you want to remove. Click **Apply** to implement the changes you have marked. If a package you want to install depends on other packages that are not installed, the utility will ask for permission to install the dependent packages. Because you need to work with **root** privileges to install and remove software, the utility may ask for the **root** password. When it is finished, the utility may ask if you want to run the new application. Close the Add/Remove Software window when you are finished. Packages you installed may be available on the Main menu.

## WHERE TO FIND DOCUMENTATION

Distributions of Linux, including Fedora/RHEL, typically do not come with hard-copy reference manuals. However, its online documentation has always been one of Linux's strengths. The *man* (or *manual*) and *info* pages have been available via the *man* and *info* utilities since early releases of the operating system. The GNOME desktop provides a graphical Help Browser. Not surprisingly, with the ongoing growth of Linux and the Internet, the sources of documentation have expanded as well. This section discusses some of the places you can look for information on Linux in general and Fedora/RHEL in particular. See also Appendix B.

![](img/f28adb66a7398a382f0505e0ba74a872_164_0.png)

**Figure 4-25** The GNOME Help Browser

## GNOME HELP BROWSER

To display the GNOME Help Browser (Figure 4-25), select **Main menu: System Help**. Click topics in this window until you find the information you are looking for. Click **Manual Pages** to display man pages. Click **GNU Info Pages** to display info pages. You can also search for a topic using the text box labeled _Search_.

## man: DISPLAYS THE SYSTEM MANUAL

In addition to the graphical GNOME Help Browser, the textual **man** utility displays (man) pages from the system documentation. This documentation is helpful when you know which utility you want to use but have forgotten exactly how to use it. You can also refer to the man pages to get more information about specific topics or to determine which features are available with Linux. Because the descriptions in the system documentation are often terse, they are most helpful if you already understand the basic functions of a utility.

Because **man** is a character-based utility, you need to open a terminal emulator window (page 118) to run it. You can also log in on a virtual terminal (page 137) and run man from there.

To find out more about a utility, give the command **man**, followed by the name of the utility. Figure 4-26 shows man displaying information about itself; the user entered a **man man** command.

The man utility automatically sends its output through a _pager_—usually **less** (page 150), which displays one screen at a time. When you access a manual page in this manner, **less** displays a colon (:) prompt at the bottom of the screen after it displays each screen of text and waits for you to request another screen of text by pressing the **SPACE** bar. Pressing **h** (help) displays a list of less commands. Pressing **q** (less(pager))

![](img/f28adb66a7398a382f0505e0ba74a872_165_0.png)

Figure 4-26 The man utility displaying information about itself

(quit) stops less and causes the shell to display a prompt. You can search for topics covered by man pages using the apropos utility (page 127).

Based on the FHS (Filesystem Hierarchy Standard; page 198), the Linux system manual and the man pages are divided into ten sections, where each section describes related tools:

- 1. User Commands
- 2. System Calls
- 3. Subroutines
- 4. Devices
- 5. File Formats
- 6. Games
- 7. Miscellaneous
- 8. System Administration
- 9. Kernel
- 10. New

This layout closely mimics the way the set of UNIX manuals has always been divided. Unless you specify a manual section, man displays the earliest occurrence in the manual of the word you specify on the command line. Most users find the information they need in sections 1, 6, and 7; programmers and system administrators frequently need to consult the other sections.

In some cases the manual contains entries for different tools with the same name. For example, the following command displays the man page for the passwd utility from section 1 of the system manual:

```
$ man passwd
```

To see the man page for the passwd file from section 5, enter this command:

```
$ man 5 passwd
```

The preceding command instructs man to look only in section 5 for the man page. In documentation you may see this man page referred to as **passwd(5)**. Use the -a option (see the adjacent tip) to view all man pages for a given subject (press **<RETURN>** to display each subsequent man page). For example, give the command man -a **passwd** to view all man pages for **passwd**.

### Options

> tip An option modifies the way a utility or command works. Options are usually specified as one or more letters that are preceded by one or two hyphens. An option typically appears following the name of the utility you are calling and a **SPACE**. Other *arguments* (page 1069) to the command follow the option and a **SPACE**. For more information refer to “Options” on page 225.

## apropos: SEARCHES FOR A KEYWORD

When you do not know the name of the command you need to carry out a particular task, you can use *apropos* with a keyword to search for it. This utility searches for the keyword in the short description line (the top line) of all *man* pages and displays those that contain a match. The *man* utility, when called with the `-k` (keyword) option, provides the same output as *apropos* (it is the same command).

The database *apropos* uses, named *whatis*, is not available on Fedora/RHEL systems when they are first installed, but is built automatically by *cron* (page 365) using *makewhatis*. (The *cron* utility runs the `/etc/cron.daily/makewhatis` *cron* script to build the *whatis* database.) If you turn the system off periodically (as with a laptop), the script may not be run. If *apropos* does not produce any output, run the command `makewhatis -w` while working with root privileges.

The following example shows the output of *apropos* when you call it with the **who** keyword. The output includes the name of each command, the section of the manual that contains it, and the brief description from the top of the man page. This list includes the utility that you need (**who**) and identifies other, related tools that you might find useful:

```
$ apropos who
at.allow (5)
	- determine who can submit jobs via at or batch
at.deny (5)
	- determine who can submit jobs via at or batch
from (1)
	- print names of those who have sent mail
w (1)
	- Show who is logged on and what they are doing.
w,procs (1)
	- Show who is logged on and what they are doing.
who (1)
	- show who is logged on
whoami (1)
	- print effective userid
whois (1)
	- client for the whois directory service
```

**whatis** The *whatis* utility is similar to *apropos* but finds only complete word matches for the name of the utility:

```
$ whatis who
who
(1) - show who is logged on
```

## info: DISPLAYS INFORMATION ABOUT UTILITIES

The textual *info* utility is a menu-based hypertext system developed by the GNU project (page 2) and distributed with Fedora/RHEL. The *info* utility includes a tutorial

### man and info display different information

> The *info* utility displays more complete and up-to-date information on GNU utilities than does *man*. When a man page displays abbreviated information on a utility that is covered by *info*, the man page refers to *info*. The *man* utility frequently displays the only information available on non-GNU utilities. When *info* displays information on non-GNU utilities, it is frequently a copy of the *man* page.

![](img/f28adb66a7398a382f0505e0ba74a872_168_0.png)

**Figure 4-27** The initial screen displayed by info coreutils

on itself (www.gnu.org/software/textinfo/manual/info) and documentation on many Linux shells, utilities, and programs developed by the GNU project. **Figure 4-27** shows the screen that *info* displays when you give the command *info coreutils* (the coreutils software package holds the Linux core utilities).

Because the information on this screen is drawn from an editable file, your display may differ from the screens shown in this section. When you see the initial info screen, you can press any of the following keys:

- **h** to go through an interactive tutorial on info
- **?** to list info commands
- **SPACE** to scroll through the menu of items for which information is available
- **m** followed by the name of the menu you want to display or a **SPACE** to display a list of menus
- **q** or **CONTROL-C** to quit

The notation info uses to describe keyboard keys may not be familiar to you. The notation **C-h** is the same as **CONTROL-H**. Similarly, **M-x** means hold down the **META** or **ALT** key and press **x**. (On some systems you need to press **ESCAPE** and then **x** to duplicate the function of **META-X**.)

### You may find pinfo easier to use than info

> The pinfo utility is similar to info but is more intuitive if you are not familiar with the emacs editor. This utility runs in a textual environment, as does info. When it is available, pinfo uses color to make its interface easier to use. If pinfo is not installed on the system, use the Add/Remove Software window (page 123) to install the **pinfo** package. Run pinfo from a terminal emulator or Run Application window (**ALT-F2**) and select **Run in terminal**.
