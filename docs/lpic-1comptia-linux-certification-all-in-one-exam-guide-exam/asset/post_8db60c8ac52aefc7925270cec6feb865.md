
## Using man Pages

One of the primary ways to maintain Linux system documentation is through the use of manual (*man*) pages. These manual pages contain documentation about the operating system itself as well as any *applications* installed on the system. These man pages are viewed using a utility called *man*.

The *man* utility was originally developed and used by the UNIX operating system. It has been ported to Linux and provides the same functionality as on a UNIX system. It can be used to display a manual page for a particular Linux command, utility, or file.

The man utility is an extremely useful tool when managing a Linux system. If you think about it, there are a lot of commands and utilities available on even the most basic Linux system. Some of the commands and utilities are used frequently; others are used very rarely. It's very difficult for the average Linux admin to remember the syntax and options used by every possible command and utility, especially those you don't use frequently.

The man utility is a real lifesaver. If you ever find yourself at a loss when working with a particular command or utility, you can use man to display the appropriate man page and remind yourself of how it's used. We love man!

In addition to system commands and utilities, man pages are also maintained for most of the packages on your system. Whenever you install a package on Linux, the man pages containing the documentation for the software are also installed. This allows you to use man to view documentation for these packages as well.

In this part of the chapter, we'll review the following man-related topics:
- The man directory structure
- Manual sections
- Using man to view documentation

## The man Directory Structure

The actual pages displayed by man are maintained in several directories beneath the directory specified in the *MANPATH* environment variable. On a 64-bit openSUSE Linux 11.3 system, the *MANPATH* variable is set to the */usr/lib64/man*:</usr/lib64/gcc/x86_64-suse-linux/4.6/man></:*/usr/local/man</:*/usr/share/man* directories. You can check the value of the *MANPATH* variable on your system by entering *echo $MANPATH* at a shell prompt. When you do, a list of environment variables is displayed. The *MANPATH* variable lists the directories containing man pages, each separated by a colon, as shown in Figure 2-8.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_76_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_77_0.png)

It’s important to note that the man utility can be implemented in different ways on different Linux distributions. For example, the Fedora distribution doesn’t use the MANPATH environment variable by default. Instead, it uses the MANPATH_MAP directive in the /etc/man_db.conf file to specify the directories where man pages are stored. An example of this configuration file is shown in Figure 2-9.

Beneath the directories specified in the MANPATH variable or in the MANPATH_MAP directive in the /etc/man_db.conf file are a series of directories denoted by man1, man2, man3, etc., as shown in Figure 2-10. Some of the directories shown in Figure 2-10 aren’t used for manual sections. Directories such as hu, it, and jp are used for man pages that have been localized into a language other than English.

## Manual Sections

All of the man pages contained in the various man directories together compose the manual. Each of the directories shown in Figure 2-10 represents a section of the manual. The standards used by man page authors divide the manual into the sections shown in Table 2-2.

Manual pages are categorized and stored in the appropriate directory, depending upon the type of software they are associated with. Many of the man pages you will use in this course will be stored in Section 1: Shell Commands and Section 8: Administrative Utilities.

| Section | Content |
| :--- | :--- |
| 1 | Programs and shell commands that can be used by any user |
| 2 | System functions provided by the Linux kernel |
| 3 | Library functions |
| 4 | Special files found in /dev |
| 5 | File format descriptions and conventions |
| 6 | Games |
| 7 | Miscellaneous conventions |
| 8 | Administrative utilities used by the root user |
| 9 | Kernel routine documentation |

Table 2-2 Sections Used in man pages

## Using man to View Documentation

Using man to look up information is really easy. All you have to do is enter man followed by the name of the utility you need information about.

For example, the ls command is a very useful shell command that you can use to display a list of files in a directory. It can be used with a variety of options that customize how it works and how the data it returns is displayed. How do you know what these options are and how to use them? You use the man utility to display the manual page for the ls command. To do this, simply enter man ls at a shell prompt. When you do, the screen shown in Figure 2-11 is displayed.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_77_1.png)

A given man page consists of several elements, as shown in Figure 2-11. Some man pages will include many sections; others will include only a few. Most man pages will include the following:

- **Title**: The title section is the first line of the man page. It lists the name of the utility, command, or file discussed in the man page followed by the section number. In Figure 2-11, notice that the first line reads LS(1). This indicates the man page describes the ls utility and is located in Section 1 of the manual. Remember from Table 2-2 that Section 1 of the manual contains manual pages for commands and utilities that all users on the Linux system can use.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_78_0.png)

Figure 2-11 Viewing the man page for the ls utility

- **NAME**: The NAME section simply displays the name of the command, file, or utility and a short abstract about what it does. In Figure 2-11, the NAME section indicates that the ls utility is used to list directory contents.
- **SYNOPSIS**: The SYNOPSIS section provides a brief description of the syntax for using a particular command or utility. If the manual page documents a configuration file, such as smb.conf, the SYNOPSIS section provides a brief overview of what the file is used for. In Figure 2-11, the SYNOPSIS section of the man page for the ls utility displays the syntax for using the command from the shell prompt. It tells you that you can enter it followed by a list of possible options and filenames.
- **DESCRIPTION**: The DESCRIPTION section provides the meat of the manual page. This section describes how the command, file, or utility works in detail. It also provides a list of options that can be used. For example, in Figure 2-11, the man page specifies that you can use the -a or --all option with the ls utility to display hidden directories and files along with normal files and directories in the file system. Without a man page, you probably would have never known that you could use the -a option with ls!

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_79_0.png)

- **AUTHOR**: The AUTHOR section displays the name of the programmer who wrote the command, utility, or service referenced in the man page. This is shown for the ls utility in Figure 2-12.
- **REPORTING BUGS**: The REPORTING BUGS section provides an e-mail address you can use to report any bugs you discover in the utility or the documentation, as shown in Figure 2-12.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_79_1.png)

Figure 2-12 Viewing additional man page sections for the ls utility

- **COPYRIGHT**: The COPYRIGHT section provides you with details about who owns the copyright to the command, utility, or service referenced in the man page. It also provides you with redistribution information, as shown in Figure 2-12.
- **SEE ALSO**: The SEE ALSO section provides you with a list of man pages or other resources that are related to the current man page. For example, in Figure 2-12, the SEE ALSO section directs the user to use info to view the complete documentation for the ls command.
- **Version Number and Revision Date**: The very last line of the man page displays the version number of the program and the revision date.

All sections other than NAME are optional. Authors are free to add new sections not shown in the preceding list if their particular program requires them. You may see man pages for other utilities or services that contain sections such as OPTIONS, FILES, ENVIRONMENT, or DIAGNOSTICS.

As you use man to display a manual page, a status indicator is shown at the very bottom of the display. This status indicator tells you what manual page is being displayed, the current line displayed, and how far into the document you are. This status indicator is shown in Figure 2-12. In this example, the status indicator shows that the ls(1) manual page is being displayed. It also indicates that line 224 is the top line currently displayed and that the current text displayed resides about 99 percent of the way through the entire document.

With a man page displayed, you can use the keystrokes shown in Table 2-3 to navigate around within the page.

Some man pages are short and concise; others are quite long and extensive. When working with a man page, you may need to search for a specific term within the page itself.

For example, if you're using the ls command, you may need to view extended information about files and directories in your file system. Notice in Figure 2-11 that by default ls displays only the names of the files or directories within the current directory. What if you need to view extended information, such as permissions, ownership, file size, or modification dates? This is called the long listing format. Which ls option can format the output in this manner?

Table 2-3
Keystrokes Used in man Pages

| Keystroke | Function |
| :--- | :--- |
| DOWN ARROW | Scrolls down one line in the page. |
| UP ARROW | Scrolls up one line in the page. |
| PAGE DOWN | Scrolls down 14 lines in the page. |
| PAGE UP | Scrolls up 14 lines in the page. |
| SPACEBAR | Scrolls down 26 lines in the page. |
| HOME | Moves you to the beginning of the page. |
| END | Moves you to the end of the page. |
| Q | Unloads the current man page and exits the man utility. |
