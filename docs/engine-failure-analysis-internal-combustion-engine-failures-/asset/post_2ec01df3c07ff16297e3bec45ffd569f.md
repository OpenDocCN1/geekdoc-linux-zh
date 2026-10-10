
# help

**help** \[ *command name* \]
Displays help for commands made available by the default Linux shell, *bash*. When typed without a command name, displays a list of all the *bash* commands for which help is available. You’ll find much more information about these commands by typing *man bash*.

# hostname

**hostname** \[ *option* \]\[ *host name* \]
When typed without options, *hostname* displays the system’s network identification name (*host name*). If you have root privileges, you can change the host name by specifying a valid host name.

## OPTIONS

| Use This Option | To Do This |
| --- | --- |
| `–a, ––alias` | Display the host name’s alias |
| `–i, ––ip-address` | Display the host’s Internet (IP) address |
| `–d, ––domain` | Display the name of the domain to which the host belongs |
| `–h, ––help` | List all options |

## EXAMPLES

| This Command | Does the Following |
| --- | --- |
| `hostname –i` | Finds out your system’s current Internet address (IP address). |
| `hostname –a` | Finds out your system’s host name alias. |

# hwclock

**hwclock** \[ *options* \]

Displays or sets the system's *hardware clock*, the time-keeping circuitry that keeps track of the date and time when your system is switched off. When typed without options (or with the **--show** option), this command displays the current time and date settings. The hardware clock differs from the *system clock*, a time-keeping routine that is part of the Linux kernel. Although the two are synchronized when you start your system, variations and anomalies in both time-keeping mechanisms can introduce variations between the system and hardware clock settings. To reset the date and time, use **hwclock**—do *not* use **date** with the **-s** switch—and then restart your system to synchronize the hardware and system clocks. You'll need root user privileges to use this command to change time (see **su** in Chapter 1).

See also date, rdate, and tzselect.

## OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `--hctosys` | Set the system clock to the current hardware clock. **Caution:** Do not use this option; instead, set the hardware clock (using `--set --date=datestring`) and reboot your system. |
| `--set --date=datestring` | Change the hardware date and time. Express the datestring using the following syntax: **MM**/**DD**/**YY** **hh:mm:ss** where **MM** is the month (expressed as a number from 01 to 12), **DD** is the day (expressed as a number from 01 to 31), **YY** is the last two digits of the year, **hh** is the hour (expressed as a number from 01 to 24), and **mm** is the minute (expressed as a number from 01 to 60). Optionally, you can express seconds, too. |
| `--show` | Display the current hardware clock setting. The date and time shown are the local time. |
| `--systohc` | Set the hardware clock to the current system time. |
| `--utc` | Specify that the hardware clock should track the time in Universal Coordinated Time (GMT). |
| `--version` | Display the version number. |

## EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `hwclock` | Displays the current hardware clock setting. |
| `hwclock --set --date='05/21/03 12:56'` | Sets the hardware clock local time to 12:56, May 21, 2003. |

# id

**id** \[ *option* \] \[ *username* \]

When typed without an option or arguments, **id** displays user ID information about yourself, including your user and group ID name and number. Use groups if you're interested only in group IDs.

## OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-g, --group` | Display the group ID only |
| `-G, --groups` | Display the supplementary groups |
| `--help` | List all options |
| `-u, --user` | Print only the user ID |
| `--version` | Display the version number |

## EXAMPLES

| This Command | Does the Following |
|---|---|
| `id` | Shows all information for the current user, including user ID, group ID, and supplemental group IDs. |

# info

**info** \[ *options* \] \[ *node* \]

Displays a text-based hypertext help system for GNU utilities, including the bash shell; the cpio archiver; the emacs text editor; the GNU file utilities; and GNU programming languages, such as gcc and awk. Unless you are familiar with the emacs text editor, you may find **info** counterintuitive and somewhat difficult to use. Almost all of the available information can also be accessed using **man**, which is easier to use. See the Commands table for the command keys you can use in the interactive mode.

## OPTIONS

| Use This Option | To Do This |
|---|---|
| `-d directory, --directory directory` | Add the specified directory to the list of directories for which **info** should search for info files |
| `-f filename, --file filename` | Display the specified info file |
| `--help` | List all options |
| `-n nodename, --node nodename` | Display the specified node within an **info** file |
| `-o filename, --output filename` | Route output to the specified file instead of displaying it on-screen |
| `--subnodes` | Display a list of subtopics |
| `--version` | Display the version number |

## COMMANDS

| Press This Key | To Do This |
|---|---|
| ? | Display all commands |
| b | Go to the beginning of the node |
| Ctrl + A | Go to the beginning of the line |
| Ctrl + L | Cancel the previous command |
| Ctrl + B | Move back one character |
| Ctrl + E | Go to the end of the line |
| Ctrl + F | Go to the beginning of the line |
| Ctrl + H | Display the Help window |
| Ctrl + N | Go to the next line |
| Ctrl + P | Go to the previous line |
| Ctrl + R | Search up within a list |
| Ctrl + S | Search down within a list |
| Ctrl + X, B | Show the history list |
| d | Display the top-level directory |
| Delete | Scroll up |
| e | Go to the end of the node |
| Esc + s | Search up within the current node |
| f | Follow a cross-reference |
| i | Search for a string in the index |
| l | Go back in the history list |
| m | Choose a menu item |
| n | Move to the next node |
| p | Move to the previous node |
| q | Quit info |
| s | Search down within the current node |
| Spacebar | Scroll down |
| t | Move to the top node |
| Tab | Skip to the next hyperlink |
| u | Move up |

## EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `info` | Starts info and displays the top-level menu. |
| `info file` | Displays the top-level menu of File Utilities. |
| `info file disk` | Displays the Disk Usage node within File Utilities. |

# man

**man** \[ *options* \] \[ *section* \] \[ *title* \]

Displays text-only manual (man) pages using the less text reader (see Chapter 8). Adhering to a standard heading format, man pages provide a quick way to get information on most of the utilities installed on your system. Man pages also include information of interest to programmers, including details concerning system and library calls. Man pages are organized into separate directories, called sections (see the Sections table). To use man, type man followed by the title of the man page you're looking for. You can also use several command options. When you're searching with the -K option, be sure to limit the scope of the search by specifying the section you want (for example, for utilities and shell commands, use Section 1).

*See also info, less (Chapter 8).*

## SECTIONS

| Section Number | Topic |
| :--- | :--- |
| 1 | Utilities and shell commands |
| 2 | System calls |
| 3 | Library calls |
| 4 | Device and other special files |
| 5 | File formats |
| 6 | Games |
| 7 | Macro packages |
| 8 | System administration commands |
| 9 | Kernel routines |

## OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `–a title` | List all the man pages that match the specified title |
| `–d` | Display debugging information |
| `–f title` | List short descriptions of all the man pages that match the specified title |
| `–h` | List all options |
| `–k string` | List short descriptions of all the man pages that match the specified string |
| `–K string` | Find and display all pages containing the specified string |
| `–M directory` | Look for man pages in the directory instead of in the default man directories |
| `–P program` | Use the specified program to display the man page |

## EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `man du` | Displays the du (disk usage) man page. |
| `man –a less` | Displays all the man pages that match the title less. |
| `man –f file` | Displays a list containing brief descriptions of all the man pages that match the title file. |
| `man 1 –K file` | Displays all the man pages from Section 1 (executable commands and utilities) that contain the word file. |
