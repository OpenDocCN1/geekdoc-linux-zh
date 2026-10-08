
# 1370

/usr/xpg4/bin/tail
The following options are supported for /usr/xpg4/bin/tail only.

-   -c number Specify number as a decimal integer whose sign affects the location in the file, measured in bytes, to begin the display.
-   + Start the display relative to the beginning of the file.
-   + Start the display relative to the end of the file.
-   none The origin for counting is 1; that is, -c +1 represents the first byte of the file, -c -1 the last.
-   -n number Equivalent to -c number, except measure starting location in the file in lines instead of bytes. The origin for counting is 1; that is, -n +1 represents the first byte of the file, -n -1 the last.

# Operands

-   file
    A path name of an input file. If you specify no file, use the standard input.

# Usage

See largefile(5) for the description of the behavior of tail when encountering files greater than or equal to 2 Gbytes (2^31 bytes).

# Examples

The following command displays the last 10 lines of the file /var/adm/sug followed by any lines that are appended to the file between the time you initiate tail and the time you call it.

```
# tail -f /var/adm/sug
SU 04/04 15:13 + pts/6 winsorroot
SU 04/04 17:25 + pts/6 winsorroot
SU 04/05 12:46 + pts/6 winsorroot
SU 04/05 12:48 + pts/6 winsorroot
SU 04/05 17:41 + pts/6 winsorroot
SU 04/06 09:46 + pts/3 winsorroot
SU 04/06 18:22 + pts/6 winsorroot
SU 04/07 08:56 + pts/6 winsorroot
SU 04/07 13:41 + pts/3 winsorroot
SU 04/07 16:17 + pts/6 winsorroot
SU 04/07 16:17 + pts/3 winsorroot
SU 04/07 16:17 + pts/3 winsorroot
SU 04/07 16:18 + pts/3 winsorroot
^C
```

The following example displays the last 15 lines of the file /var/adm/sug followed by any lines that are appended to the file between the time you initiate tail and the time you call it.

```
# tail -15cf /var/adm/sug
/3 winsorroot
SU 04/07 16:22 + pts/5 winsorroot
```

# tail

# 1371

```
SU 04/07 16:23 + pts/5 winsor-root
SU 04/07 16:24 + pts/5 winsor-root
C
```

The following example displays the contents of the file kookaburra-2 in order.

```
castle# tail -r kookaburra-2
8 Leave some there for me.
7 Stop, kookaburra, stop, kookaburra
6 Eating all the gumdrops he can see.
5 Kookaburra sits in the old gum tree
```

```
4 Gay your life must be.
3 Laugh, kookaburra, laugh, kookaburra
2 Merry merry king of the bush he is.
1 Kookaburra sits in the old gum tree
castle%
```

# Environment Variables

See environ(5) for the messages of the following environment variables that affect the execution of tail: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

```
0 Successful completion.
>0 An error occurred.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

```
/usr/bin/tail
```

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNmxcu |
| CSI | Enabled |

```
/usr/xpg4/bin/tail
```

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNmxcu4 |
| CSI | Enabled |

# See Also

```
cat(1), head(1), more(1), pg(1), dd(1M), attributes(5), environ(5),
largefile(5), XPG4(5)
```

# 1372

# talk

# talk — Talk to Another User

# Synopsis

```
/usr/bin/talk address [terminal]
```

# Description

The talk command is a two-way, screen-oriented similar communication program.
When you first invoke it, talk sends a message similar to the following to the specified address.

```
Message from TalkDaemon@her-system at time...
talk: connection requested by your-address
talk: respond your-address
```

At this point, the recipient of the message can reply by typing:
talk your-address

Once communication is established, the two parties can talk simultaneously with their output displayed in separate regions of the screen. Characters are processed as follows.

-   * The alert character alerts the recipient's terminal.
-   Control-L refreshes the screen's regions.
-   The erase and kill characters affect the sender's terminal in the manner described by the termios(3) interface.
-   The interrupt or end-of-file characters terminate the local talk command. Once the talk session has been terminated on one side, the other side of the talk session is notified that the talk session has been terminated and is able to do nothing except.
-   Typing characters from the print or space LC_CTYPE classifications sends those characters to the recipient's terminal.
-   When and only the stty local mode is enabled, additional special control characters and multibyte or single-byte characters are processed as printable characters if their wide-character equivalents are printable.
-   Typing nonprintable characters writes them to the recipient's terminal: control characters appear as a caret (^) followed by the appropriate ASCII character, and with the high-bit set apart in "meta" notation. For example, \003 is displayed as ^C and \372 as M-z.

You can grant or deny permission to be a recipient of a talk message.

# 1402

# talk 1373

# Note — Typing characters de-clutters the screen.

# Operands

-   address: Specify the recipient.
-   terminal: Specify the terminal.

# Environment Variables

See environ(5) for the messages of the following environment variables that affect the execution of tail: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

```
0 Successful completion.
>0 An error occurred.
```

# Files

-   /etc/hosts: Host-name.
-   /var/adm/utm: User information.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNmxcu |

# See Also

```
mail(1), mesg(1), pr(1), stty(1), who(1), write(1), termios(3), attributes(5), environ(5)
```

# 1374

# tar

# tar — Create Archives and Extract Files

# Synopsis

```
/usr/bin/tar [rtufFiknopqvw@ (2^31 bytes)] [tarfile]
```

New!

Description
The advantages of the tar command is that it is available on Unix systems and that public domain versions are readily available. The disadvantages of the tar command are that it is not aware of file boundaries, full path-name cannot exceed 255 characters, it does not copy empty directories or special files, and it cannot be used to create multiple volumes.

The tar command creates archives from a single file called a tarfile. A tarfile is usually magnetic but it can be used. tar with the key argument, which is a set of characters containing exactly one letter–c (create), r (replace), t (table of contents), u (update), or x (extract)—and zero or more function modifiers (letters or digits), depending on the letter used. The key string contains no space characters. Function modifiers are listed in the command line in the order as their function modifiers appear in the key string.

-I include-file, -C directory file, and file specify which files or directories are to be archived or extracted. In all cases, appearance of a directory name refers to files and (recursively) subdirectories of that directory. Arguments appearing within braces you must specify one of the arguments.

# Notes

You cannot access the n-th occurrence of a file.
Taper are handled ungracefully.
When the Volume Management daemon is running, accesses to disk devices through the conventional device names (for example, /dev/rdiskette) may not succeed. See void(1) for further details.

The tar archive format allows UIDs and GIDs up to 2097151 to be stored in the archive header. Files with UIDs and GIDs greater than this value are archived with the UID and GID of 60001 (nobody).

If you create an archive that contains files whose names are created by processes running in multiple locations, use a single local with a 8-bit codeset (for example, us local) to both create the archive and extract files from it.

*
