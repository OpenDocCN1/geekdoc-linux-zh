# Man Pages

*Man* (short for "manual") *pages* are online documents that describe the format and functioning of commands and files as well as some other tools available on your Linux system. Man pages are not meant to be comprehensive but rather to give general information about usage. Man pages aren't meant to take the place of the source documentation, but instead to highlight how to use the referenced resource. Unless the system was installed without them, man pages are readily available from the command line. Simply type man man to get the man page on how to use man pages. The basic format of the command is:

```
man [options] [section] topic
```

There is a configuration file for the man command located at /etc/man.config. This file allows you to configure the environment variables that the man command uses if you don't wish to specify them on the command line. The options include the path that should be searched for man pages, the order in which the manual sections should be searched, and whether to store the man pages in a compressed format.

Man pages are grouped into sections or categories as outlined in Table 4.1. A given command can have man pages in different categories if appropriate; for example, the umount command has a page in section 2 for the programmer's system call and a page in section 8 for its use as a system administration tool. Some packages, like Tcl, separate their pages into a different section rather than including them in the categories listed.

Table 4.1: Online Manual Sections Specified in the man Command

| Section | Category |
|---|---|
| 1 | User commands that may be started by anyone |
| 2 | System calls (kernel functions) |
| 3 | Library functions |
| 4 | Devices |
| 5 | File format descriptions |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System administration tools that only root can execute |
| 9 | More kernel routine documentation |
| n | New documentation that may be recategorized |
| o | Old documentation that may go away soon |
| l | Documentation referring to this specific system |

If you don't remember the name of the command you want to know about, man has an option that will look for a keyword in the Whatis database, a set of files containing short descriptions of system commands. In this way, if you know that the purpose of the command you want is to add a user, you can specify:

```
$ man -k user
```

The output, an excerpt of which is listed below, will be a list of man page topics that contain the word user in the description, along with the section each page is in and a simple description of the topic.