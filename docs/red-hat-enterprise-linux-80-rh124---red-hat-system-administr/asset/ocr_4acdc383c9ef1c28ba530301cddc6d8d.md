# READING MANUAL PAGES

# OBJECTIVES

After completing this section, you will be able to find information in local Linux system manual pages.

# INTRODUCING THE MAN COMMAND

One source of documentation that is generally available on the local system is system manual pages or man pages These pages are shipped as part of the software packages for which they provide documentation, and can be accessed from the command line using the man command.

The historical Linux Programmer's Manual, from which man pages originate, was large enough to be multiple printed sections. Each section contains information about a particular topic.

# Common Sections of the Linux Manual

| SECTION | CONTENT TYPE |
|---|--|
| 1 | User commands (both executable and shell programs) |
| 2 | System calls (kernel routines invoked from user space) |
| 3 | Library functions (provided by program libraries) |
| 4 | Special files (such as device files) |
| 5 | File formats (for many configuration files and structures) |
| 6 | Games (historical section for amusing programs) |
| 7 | Conventions, standards, and miscellaneous (protocols, file systems) |
| 8 | System administration and privileged commands (maintenance tasks) |
| 9 | Linux kernel API (internal kernel calls) |

To distinguish identical topic names in different sections, man page references include in parentheses after the topic. For example, passwd(1) describes the command to change passwords, while passwd(5) explains the /etc/passwd file for storing local user accounts.

To read specific pages, use man topic. Contents are displayed one screen at a time. The man command searches manual sections in alphabetic order. For example, man passwd displays passwd(1) by default. To display the man topic from a specific section, include the section number: man 5 displays passwd(5).

# NAVIGATE AND SEARCH MAN PAGES

The ability to efficiently search for topics and navigate man pages is a critical administration skill. GUI tools make it easy to configure common system resources, but using the command-line