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

# TABLE 1.1 System V Unix Man Page Organization

Man pages in different sections might have the same name, so you might need to specify in which section to find the page. In addition, sometimes you’ll be looking for a user-level command and find a match in Section 2 or 3. Those aren’t what you seek; they’re specifically for Unix programmers, as you can see in the table.

+   1. The mkdir man page is succinct and exemplary. Here’s what you’ll see when you enter the man mkdir command:

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