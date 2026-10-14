
## Table 5-1: Man Page Organization

| Section | Contents |
|---|---|
| 1 | User commands |
| 2 | Programming interfaces for kernel system calls |
| 3 | Programming interfaces to the C library |
| 4 | Special files such as device nodes and drivers |
| 5 | File formats |
| 6 | Games and amusements such as screensavers |
| 7 | Miscellaneous |
| 8 | System administration commands |

Sometimes we need to look in a specific section of the manual to find what we are looking for. This is particularly true if we are looking for a file format that is also the name of a command. If we don’t specify a section number, we will always get the first instance of a match, probably in section 1. To specify a section number, we use man like this:

```
man section search_term
```

For example:

```
[me@linuxbox ~]$ man 5 passwd
```

will display the man page describing the file format of the /etc/passwd file.

## apropos—Display Appropriate Commands

It is also possible to search the list of man pages for possible matches based on a search term. Though crude, this approach is sometimes helpful. Here is an example of a search for man pages using the search term floppy:

```
[me@linuxbox ~]$ apropos floppy
create_floppy_devices (8)  - udev callout to create all possible
floppy devices based on the CMOS type
fdformat              (8)  - Low-level formats a floppy disk
floppy                (8)  - format floppy disks
gfloppy               (1)  - a simple floppy formatter for the GNOME
mbadblocks            (1)  - tests a floppy disk, and marks the bad
blocks in the FAT
mformat               (1)  - add an MSDOS filesystem to a low-level
formatted floppy disk
```

The first field in each line of output is the name of the man page, and the second field shows the section. Note that the man command with the -k option performs exactly the same function as apropos.

## whatis—Display a Very Brief Description of a Command

The whatis program displays the name and a one-line description of a man page matching a specified keyword:

```
[me@linuxbox ~]$ whatis ls
ls (1) - list directory contents
```

## THE MOST BRUTAL MAN PAGE OF THEM ALL

As we have seen, the manual pages supplied with Linux and other Unix-like systems are intended as reference documentation and not as tutorials. Many man pages are hard to read, but I think that the grand prize for difficulty has to go to the man page for bash. As I was doing my research for this book, I gave it a careful review to ensure that I was covering most of its topics. When printed, it's over 80 pages long and extremely dense, and its structure makes absolutely no sense to a new user.

On the other hand, it is very accurate and concise, as well as being extremely complete. So check it out if you dare, and look forward to the day when you can read it and it all makes sense.

## info—Display a Program's Info Entry

The GNU Project provides an alternative to man pages called info pages. Info pages are displayed with a reader program named, appropriately enough, info. Info pages are hyperlinked much like web pages. Here is a sample:

```
File: coreutils.info, Node: ls invocation, Next: dir invocation, Up: Directory listing
```

### 10.1 'ls': List directory contents

The 'ls' program lists information about files (of any type, including directories). Options and file arguments can be intermixed arbitrarily, as usual.

For non-option command-line arguments that are directories, by default 'ls' lists the contents of directories, not recursively, and omitting files with names beginning with '.'. For other non-option arguments, by default 'ls' lists just the filename. If no non-option argument is specified, 'ls' operates on the current directory, acting as if it had been invoked with a single argument of '.'.

The info program reads info files, which are tree-structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move you from node to node. A hyperlink can be identified by its leading asterisk and is activated by placing the cursor upon it and pressing the ENTER key.

To invoke info, enter info followed optionally by the name of a program. Table 5-2 lists commands used to control the reader while displaying an info page.

### Table 5-2: info Commands

| Command | Action |
|---|---|
| ? | Display command help. |
| PAGE UP or BACKSPACE | Display previous page. |
| PAGE DOWN or Spacebar | Display next page. |
| n | Next—Display the next node. |
| p | Previous—Display the previous node. |
| u | Up—Display the parent node of the currently displayed node, usually a menu. |
| ENTER | Follow the hyperlink at the cursor location. |
| q | Quit. |

Most of the command-line programs we have discussed so far are part of the GNU Project’s coreutils package, so you can find more information about them by typing

```
[me@linuxbox ~]$ info coreutils
```

which will display a menu page containing hyperlinks to documentation for each program provided by the coreutils package.

## README and Other Program Documentation Files

Many software packages installed on your system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plaintext format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a .gz extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless, which will display the contents of gzip-compressed text files.
