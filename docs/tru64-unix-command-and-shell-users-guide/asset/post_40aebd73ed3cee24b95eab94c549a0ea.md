
4. Enter your new password again. As before, the new password entry does not appear on the screen. When the shell prompt returns to the screen, your new password is in effect.

If you attempt to change your password and the new password does not conform to password regulations, you receive a message stating the specific problem and the restrictions in effect for the system. The exact messages and the level of detail in the descriptions provided are determined by the security and access control mechanisms in effect on your system.

> **Note**
> 
> Try to remember your password because you cannot log in to the system without it. If you forget your password, see your system administrator.

## 1.6 Getting Help

This book discusses the entry and execution of commands from the command line. If you are using any of the numerous graphical user interfaces (GUIs) that are available, see the users instructions that accompany your window manager, or see your system administrator.

Many of the basic operating system commands needed for your work are described in this book. If you want to learn more about these and other commands, see the reference pages. The reference pages are provided in several formats:

- On line (see Section 1.6.1)
- In hard copy (see Related Documents)
- In Hypertext Markup Language (HTML) format

Ask your system administrator what optional formats are installed on your system. When the hard copy documents and HTML are unavailable, you quickly can access online command documentation by using the following commands:

- The man command displays online reference pages.
- The apropos command displays a one line summary of each command pertaining to a specified subject.

The following sections describe these features.

### 1.6.1 Displaying and Printing Online Reference Pages (man)

Online reference pages contain information about commands. To view a reference page on line, use the man command. Example 1–2 shows how to view the reference page for the date command (your screen display may vary):

# Example 1-2: Reference Page for date Command

```
$ man date

date(1)                                                                 date(1)

NAME
    date - Displays or sets the date

SYNOPSIS

Without Superuser Authority - Displays the Date

date [-u] [+field_descriptor ...]

With Superuser Authority - Sets the Date

date [-nu] [MMddhhmm.sssy|alternate_date_format] [+field_descriptor ...]

Using XPG4-UNIX - Sets or Displays the Date

date [-u] mmddHHMM[yy]

date [-u] [+field_descriptor ...]

Using the Century Field Provided by Compaq - Sets the Date

date mmddHHMM[[cc]yy][.ss]

date [[cc]yy]mmddHHMM[.ss]

date mmddHHMM[.ss[[cc]yy]]

STANDARDS

Interfaces documented on this reference page conform to industry standards as follows:

date: XPG4, XPG4-UNIX

Refer to the standards(5) reference page for more information about industry standards and associated tags.

man aabima (7%)
```

The symbol man aabima (7%) at the bottom of the page indicates that 7% of the reference page is currently displayed. At this point, you can press the Space bar to display the next screen of information, press the Return key to display one more line of information, or enter q to quit and return to the shell prompt.

Use the following command format to print a reference page:

```
man manpage | lpr -P printer_name
```

For example, to print the reference page for the date command on a specific printer, enter:

```
$ man date | lpr -Pprinter_name
```

The reference page for the date command is now queued for printing on printer_name. See Section 3.3 for more information about the lpr command.

To display a brief, one-line description of a command, use the man -f command. For example, to display a brief description of the who command, enter:

```
$ man -f who
who (1)   - Identifies users currently logged in
$
```

For complete information on the man command and its options, you can display the reference page by entering the following:

```
$ man man
```

### 1.6.2 Locating Commands Using Descriptive Keywords

The apropos command and the man -k command are useful tools if you forget a command name.

Note

> The apropos and the man -k commands require access to the whatis database. This database is available if your system manager loaded the default whatis database when the operating system was installed or created the database later using the catman command.

The apropos and man -k commands perform the same function. These commands let you enter a command description in the form of keywords. The commands then list all the reference pages that contain any of the keywords.

As shown in the example, if a command description contains more than one word, the words must be enclosed in single quotes ( ' ) or double quotes ( " ). If the command description contains only one word, it is not necessary to enclose the descriptive word in quotes.

Assume that you cannot remember the name of the command that displays who is logged in to the system. To display the names and descriptions of all reference pages that have something to do with displaying users who are logged in, enter one of the following:

```
$ apropos "logged in"
```
