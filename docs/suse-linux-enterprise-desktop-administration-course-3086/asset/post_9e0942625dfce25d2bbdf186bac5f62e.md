
![](img/9129877170834ca9d5fdac5319bf5f12_94_0.png)

Manual pages whose output is marked with “p” are POSIX manual pages of the uname command (uname (1p)) and the function (uname (3p)). POSIX (Portable Operating System Interface for Unix) was developed from the IEEE and the Open Group for UNIX as a standardized interface between the application and operating system.

In SUSE Linux Enterprise Server, the manual pages are located in the directory /usr/share/man/.

If you enter man -k keyword or apropos keyword, a list of manual pages in which the keyword appears in the NAME section is displayed. For example:

![](img/9129877170834ca9d5fdac5319bf5f12_94_1.png)

```text
gecko@a30:~> man -k printf
vsprintf (3) - print to allocated string
vwprintf (3p) - wide-character formatted output of a
standard argument list
vfprintf (3) - formatted output conversion
sprintf (3) - formatted output conversion
format (n) - format a string in the style of sprintf
swprintf (3) - formatted wide character output conversion
asprintf (3) - print to allocated string
vsprintf (3p) - format output of a stdarg argument list
printf (3p) - print formatted output
sprintf (3p) - formatted output
wprintf (3p) - print formatted wide-character output
vdprintf (3) - print to a file descriptor
fwprintf (3) - formatted wide character output conversion
sprintf (3) - formatted output conversion
dprintf (3) - print to a file descriptor
wdprintf (3) - formatted wide character output conversion
printf (3) - formatted output conversion
...
```

![](img/9129877170834ca9d5fdac5319bf5f12_94_2.png)

## Exercise 3-1: Access and Use man Pages

In this exercise, use the whatis and man commands to get information on the info command. In the manual page, look for filename.

### Detailed Steps to Complete This Exercise

- 1. From the GNOME desktop, open the main menu.
- 2. Select More Applications.
- 3. In the Filter text box, enter term.
- 4. Select the GNOME Terminal icon to start a terminal emulation.
- 5. Find the sections of the man pages for the info command by entering
- `whatis info`
- 6. Read the first section (executable programs and shell commands) of the man pages of the command info by entering
- `man 1 info`
- 7. To look for filename, enter `/filename`.
- 8. Scroll through the text with the up and down arrow keys.
- 9. When you finish viewing the information, exit (quit) the man page by typing `q`.

Leave the terminal window open for the next exercise.

## Objective 2—Use info Pages

Unfortunately, a whole series of programs are no longer provided with manual pages (or the pages have become outdated). Instead, info files are used, which can be read with the `info` command.

In SUSE Linux Enterprise Desktop, the info files are located in the directory `/usr/share/info/`. The following is the beginning of the info file for the `info` command:

```
File: info.info, Node: Top, Next: Getting Started, Up:
(dir)

Info: An Introduction
*********************

Info is a program, which you are using now, for reading documentation
of computer programs. The GNU Project distributes most of its online
manuals in the Info format, so you need a program called “Info
reader” to read the manuals. One of such programs you are using now.

If you are new to Info and want to learn how to use it, type the
command ‘h’ now. It brings you to a programmed instruction sequence.

To learn advanced Info commands, type ‘n’ twice. This brings you
to ‘Info for Experts’, skipping over the ‘Getting Started’ chapter.

* Menu:

* Getting Started:: Getting started using an Info reader.
* Advanced Info::  Advanced commands within Info.
* Creating an Info File:: How to make your own Info file.
* Index::          An index of topics, commands, and variables.
```

The following are advantages of the info file format:

- It uses a structured document setup.
- Specific sections can be reached directly from the table of contents.
- Specific sections can be linked.

| Key Command | Description |
|---|---|
| Space, PageDown | Page down one screen. |
| Backspace, PageUp | Page up one screen. |
| b | Move cursor to the beginning of current info page. |
| e | Move cursor to the end of current info page. |
| Tab | Move cursor to the next reference (*). |
| Enter | Follow the reference. |
| n | Move to the next info page of the same level (Next:). |
| p | Move to the previous info page of the same level. |
| u | Move one level higher. |
| l | Move back to the last text displayed; end help. |
| s | Search in the info page. |
| h | Display help. |
| ? | List a summary of commands. |
| q | End display of info document. |

Table 3-4

![](img/9129877170834ca9d5fdac5319bf5f12_96_0.png)

## Exercise 3-2: Access and Use info Pages

In this exercise, use the `info` command to get information on info and navigate through the info text.

### Detailed Steps to Complete This Exercise

- 1. From the terminal window, display the info pages for the `info` command by entering `info info`.
- 2. Move the cursor to the first reference (Getting Started) by pressing `Tab`.
- 3. Follow the reference by pressing `Enter`.
- 4. Move the cursor to the reference Quitting Info by pressing `Tab` nine times.
- 5. Follow the reference by pressing `Enter`.
- 6. Return to the page Getting Started by typing `l` (lowercase L).
- 7. Exit the info file by typing `q`.
- 8. Close the terminal window.

## Objective 3—Access Release Notes and White Papers

Release notes, white papers, and other sources of helpful information are stored in the directory `/usr/share/doc/`. This directory contains the following:

- Release Notes
- Manuals
- Help for Installed Packages
- HOWTOs

### Release Notes

When you complete the installation of SUSE Linux Enterprise Server, the release notes appear in a window. See Figure 3-1.

![](img/9129877170834ca9d5fdac5319bf5f12_97_0.png)

Figure 3-1

If you want to access these release notes later, you can find them in various languages in the directory `/usr/share/doc/release-notes/SUSE_Linux_Enterprise_Desktop_10/`. As visible in Figure 3-1, these files point to the address where you find the up-to-date release notes, `http://www.novell.com/documentation/sled10/readme/release_notes_sp1.html`.

### Manuals

The administration manual is also installed during the installation of SUSE Linux Enterprise Desktop 10.

A PDF version of the manual is in `/usr/share/doc/manuals/sled-deployment_en/`. If you prefer HTML, an HTML version is available in the `manuals/subfolder`.

### Help for Installed Packages

Help files are available in the following directory for most installed packages: `/usr/share/doc/packages/package-name/`.

These help files are written by the programmers of the package. Therefore, the format of these files is not standardized. Some packages provide help files in HTML, while others are in regular ASCII.

### HOWTOs

You can find additional information (including background material) in the howtos. A howto is available for almost every imaginable topic in Linux.

You can find a list of all current howtos (together with available translations) at `http://www.tldp.org/`.

## Objective 4—Use GUI-Based Help

An online help tool is also available for graphical applications of SUSE Linux Enterprise Desktop 10. See Figure 3-2.

To start the online help, select **Computer > More Applications > System > Yelp**.

Use the links to navigate through the content.

You can also use the search function to speed up your search for help. Enter a topic in the Search text box in the tool bar and press Enter.

The online help is available in most GNOME applications and can be started by pressing F1.

![](img/9129877170834ca9d5fdac5319bf5f12_98_0.png)

![](img/9129877170834ca9d5fdac5319bf5f12_99_0.png)

Figure 3-2

## Objective 5—Find Help on the Web

You can find an extensive collection of information about Linux on the Internet for both general and special issues. The following are some of the more frequently used Linux sites:

- *http://www.novell.com/linux/*
- *http://www.tldp.org*
- *http://www.cert.org* (especially for security issues)
- *http://www.securityfocus.com* (especially for security issues)
- *http://www.kernel.org* (especially for issues in connection with the Linux kernel)
- *http://www.novell.com/coolsolutions/* (follow the links on Linux)
