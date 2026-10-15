
too, has its own unique layout, such as sections 9E, 9F, and 9S, which deal with device drivers, and a complete lack of Section 6 (games). On any Unix system, the command man man (get it? The manual for the manual) will give you the complete synopsis.

| Section | Category |
|---|---|
| 1 | User commands |
| 1M | System maintenance commands |
| 2 | System calls |
| 3 | Library routines |
| 4 | Administrative files |
| 5 | Miscellaneous |
| 6 | Games |
| 7 | I/O and special files |
| 8 | Administrative commands |

## TABLE 1.1 System V Unix Man Page Organization

Man pages in different sections might have the same name, so you might need to specify in which section to find the page. In addition, sometimes you’ll be looking for a user-level command and find a match in Section 2 or 3. Those aren’t what you seek; they’re specifically for Unix programmers, as you can see in the table.

- 1. The mkdir man page is succinct and exemplary. Here’s what you’ll see when you enter the man mkdir command:

Click here to view code image

```
% man mkdir

MKDIR(1)                 FreeBSD General Commands Manual
Manual                   MKDIR(1)

NAME
    mkdir - make directories

SYNOPSIS
    mkdir [-p] [-m mode] directory_name ...

DESCRIPTION
    Mkdir creates the directories named as operands, in the order specified, using mode rwxrwxrwx (0777) as modified by the current umask(2).

    The options are as follows:

    -m   Set the file permission bits of the final created directory to the specified mode. The mode argument can be in any of the formats specified to the chmod(1) command. If a symbolic mode is specified, the operation characters "+" and "-" are interpreted relative to an initial mode of "a=rwx".
```

-p Create intermediate directories as required. If this option is not specified, the full path prefix of each operand must already exist. Intermediate directories are created with permission bits of rwxrwxrwx (0777) as modified by the current umask, plus write and search permission for the owner.

The user must have write permission in the parent directory.

## DIAGNOSTICS

The mkdir utility exits 0 on success, and >0 if an error occurs.

## SEE ALSO

rmdir(1)

## STANDARDS

The mkdir utility is expected to be IEEE Std1003.2 ("POSIX.2") compatible.

## HISTORY

A mkdir command appeared in Version 1 AT&T UNIX.

## Note

Notice in the example that in the first line, the command itself is in boldface type, but everything else is not bold. Throughout this book, whenever an example contains both user input and Unix output, the user input is bold so that you can easily spot what you are supposed to enter.

The very first line of the output tells me that it’s found the mkdir command in Section 1 (user commands) of the man pages, with the middle phrase, FreeBSD General Commands Manual, indicating that I’m running on a version of Unix called FreeBSD. The NAME section always details the name of the command and a one-line summary of what it does. SYNOPSIS explains how to use the command, including all possible command flags and options.

DESCRIPTION is where all the meaningful information is, and it can run on for dozens of pages, explaining how complex commands such as csh or vi work. SEE ALSO suggests other commands that are related in some way. The Revision line at the bottom is different on each version of man, and it indicates the last time, presumably, that this document was revised.

2. The same man page from an Oracle Solaris workstation is quite different, as shown in Figure 1.1.

## User Commands

mkdir(1)

## NAME

mkdir - make directories

## SYNOPSIS

```
/usr/bin/mkdir [-m mode] [-p] dir...
```

## DESCRIPTION

The mkdir command creates the named directories in mode 777 (possibly altered by the file mode creation mask umask(1)).

Standard entries in a directory (for instance, the files ".", for the directory itself, and "..", for its parent) are made automatically. mkdir cannot create these entries by name. Creation of a directory requires write permission in the parent directory.

The owner-ID and group-ID of the new directories are set to the process's effective user-ID and group-ID, respectively. mkdir calls the mkdir(2) system call.

## setgid and mkdir

To change the setgid bit on a newly created directory, you must use chmod g+s or chmod g-s after executing mkdir.

The setgid bit setting is inherited from the parent directory.

## OPTIONS

The following options are supported:

- -m mode  This option allows users to specify the mode to be used for new directories. Choices for modes can be found in chmod(1).

- -p  With this option, mkdir creates dir by creating all the non-existing parent directories first. The mode given to intermediate directories is the difference between 777 and the bits set in the file mode creation mask. The difference, however, must be at least 300 (write and execute permission for the user).

## OPERANDS

The following operand is supported:

# FIGURE 1.1 mkdir man page on an Oracle Solaris system.

3. Not sure of a specific command? That’s where man -k or its alias apropos comes in handy:

Click here to view code image

```
% man -k date | head -18
1. date(1) /usr/share/man/man1/date.1
date - write the date and time
```
