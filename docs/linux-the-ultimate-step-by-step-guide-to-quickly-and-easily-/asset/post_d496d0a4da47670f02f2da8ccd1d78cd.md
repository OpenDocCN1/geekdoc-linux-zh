
This is the first function speaking...
This is now the second function speaking...

To remove the definition of a function from the shell, you use the `unset` command with the `-f` option. This is the same command you use to remove the definition of a variable to the shell.

$ unset -f function_name

## Unix - Pipes and Filters

You can connect two commands together so that the output from one program becomes the input of the next program. Two or more commands connected in this way form a *pipe*. To make a pipe, put a vertical bar (|) on the command line between two commands. When a program takes its input from another program, performs some operation on that program, and writes the result to the standard output, it is referred to as a *filter*.

## The grep Command

The `grep` program searches a file or files for lines that have a certain pattern. The syntax is –

$ grep pattern file(s)

The name “grep” derives from the `ed` (a UNIX line editor) command `g/re/p`, which means, “globally search for a regular expression and print all lines containing it.” A regular expression is either plain text (a word, for example) and/or special characters used for pattern matching. The simplest use of `grep` is to look for a pattern consisting of a single word. It can be used in a pipe so that only those lines of the input files containing a given string are sent to the standard output. If you do not give `grep` a filename to read, it reads its standard input; that is the way all filter programs work –

$ ls -l | grep "Aug"
-rw-rw-rw- 1 john doc 11008 Aug 6 14:10 ch02
-rw-fw-rw- 1 john doc 8515 Aug 6 15:30 ch07
-rw-rw-r-- 1 john doc 2488 Aug 15 10:51 intro
-rw-rw-r-- 1 carol doc 1605 Aug 23 07:35 macros

There are various options, which you can use along with `grep` command –

| Option | Description |
| :----- | :---------- |
| -v | Print all lines that do not match pattern. |
| -n | Print the matched line and its line number. |
| -l | Print only the names of files with matching lines (letter “l”) |
| -c | Print only the count of matching lines. |
| -i | Match either upper- or lowercase. |

Next, let’s use a regular expression that tells `grep` to find lines with “carol”, followed by zero or more other characters abbreviated in a regular expression as “.*”), then followed by “Aug”. Here we are using -i option to have case insensitive search –

$ ls -l | grep -i “carol.*aug”
-rw-rw-r-- 1 carol doc 1605 Aug 23 07:35 macros

## The sort Command

The sort command arranges lines of text alphabetically or numerically. The example below sorts the lines in the food file –

$ sort food
Afghani Cuisine
Bangkok Wok
Big Apple Deli
Isle of Java
Mandalay
Sushi and Sashimi
Sweet Tooth
Tío Pepe’s Peppers

The sort command arranges lines of text alphabetically by default. There are many options that control the sorting –

| Option | Description |
| :----- | :---------- |
| -n | Sort numerically (example: 10 will sort after 2), ignore blanks and tabs. |
| -r | Reverse the order of sort. |
| -f | Sort upper- and lowercase together. |
| +x | Ignore first x fields when sorting. |

More than two commands may be linked by a pipe. Taking a previous pipe example using grep, we can further sort the files modified in August by order of size.

The following pipe consists of the commands ls, grep, and sort –

$ ls -l | grep “Aug” | sort +4n
-rw-fw-r- 1 carol doc 1605 Aug 23 07:35 macros
-rw-fw-r- 1 john doc 2488 Aug 15 10:51 intro
-rw-fw-r- 1 john doc 8515 Aug 6 15:30 ch07
-rw-fw-r- 1 john doc 11008 Aug 6 14:10 ch02

This pipe sorts all files in your directory modified in August by order of size, and prints them to the terminal screen. The sort option +4n skips four fields (fields are separated by blanks) then sort the lines in numeric order.

## The pg and more Commands

A long output would normally zip by you on the screen, but if you run text through more or pg as a filter, the display stops after each screen of text. Let us assume that you have a long directory listing. To make it easier to read the sorted listing, pipe the output through more as follows –

$ ls -l | grep "Aug" | sort +4n | more
-rw-fw-r- 1 carol doc 1605 Aug 23 07:35 macros
-rw-fw-r- 1 john doc 2488 Aug 15 10:51 intro
-rw-fw-r- 1 john doc 8515 Aug 6 15:30 ch07
-rw-fw-r- 1 john doc 14827 Aug 9 12:40 ch03
.
.
.
-rw-fw-r- 1 john doc 16867 Aug 6 15:56 ch05
--More--(74%)

The screen will fill up with one screen of text consisting of lines sorted by order of file size. At the bottom of the screen is the more prompt where you can type a command to move through the sorted text. When you are done with this screen, you can use any of the commands listed in the discussion of the more program.

# Chapter Sixteen: UNIX USEFUL COMMAND

This quick guide lists commands, including a syntax and brief description. For more detailed information check out commands man page.

$ man command

## Files and Directories

These commands allow you to create directories and handle files.

| Command | Description |
| :--- | :--- |
| cat | Display File Contents |
| cd | Changes Directory to dirname |
| chgrp | Change file group |
| chmod | Changing Permissions |
| cp | Copy source file into destination |
| file | Determine file type |
| find | Find files |
| grep | Search files for regular expressions. |
| head | Display first few lines of a file |
| ln | Create softlink on oldname |
| ls | Display information about file type. |
| mkdir | Create a new directory dirname |
| more | Display data in paginated form. |
| mv | Move (Rename) a oldname to newname. |
| pwd | Print current working directory. |
| rm | Remove (Delete) filename |
| rmdir | Delete an existing directory provided it is empty. |
| tail | Prints last few lines in a file. |
| touch | Update access and modification time of a file. |

| Command | Description |
| :--- | :--- |
| awk | Pattern scanning and processing language |
| cmp | Compare the contents of two files |
| comm | Compare sorted data |
| cut | Cut out selected fields of each line of a file |
| diff | Differential file comparator |
| expand | Expand tabs to spaces |
| join | Join files on some common field |
| Perl | Data manipulation language |
| sed | Stream text editor |
| sort | Sort file data |
| split | Split file into smaller files |
| tr | Translate characters |
| uniq | Report repeated lines in a file |
| wc | Count words, lines, and characters |
| vi | Opens vi text editor |
| vim | Opens vim text editor |
| fmt | Simple text formatter |
| spell | Check text for spelling error |

## Manipulating data

The contents of files can be compared and altered with the following commands.

## Compressed Files

Files may be compressed to save space. Compressed files can be created and examined -

| Command | Description |
| :--- | :--- |
| ispell | Check text for spelling error |
| Emacs | GNU project Emacs |
| ex, edit | Line editor |
| gunzip | Uncompress gzipped files |
| uncompress | Uncompress files |
| zcat | Cat a compressed file |
| zdiff | Compare compressed files |

## Getting Information

Various Unix manuals and documentation are available on-line. The following Shell commands give information –

| Command | Description |
| :--- | :--- |
| apropos | Locate commands by keyword lookup |
| info | Displays command information pages online |
| man | Displays manual pages online |
| whatis | Search the whatis database for complete words. |
| yelp | GNOME help viewer |

## Network Communication

The following commands are used to send and receive files from a local UNIX hosts to the remote hosts around the world.

| Command | Description |
| :--- | :--- |
| ftp | File transfer program |
| rcp | Remote file copy |
| rlogin | Remote login to a UNIX host |
| rsh | Remote shell |
| tftp | Trivial file transfer program |
| telnet | Make terminal connection to another host |
| ssh | Secure shell terminal or command connection |
| scp | Secure shell remote file copy |
| sftp | secure shell file transfer program |

Some of these commands may be restricted on your computer for security reasons.

## Messages between Users

The UNIX system supports on-screen messaging to other users and worldwide electronic mail –

| Command | Description |
| :--- | :--- |
| Evolution | GUI mail handling tool on Linux |
| mail | Simple send or read mail program |
| mesg | Permit or deny messages |
| parcel | Send files to another user |
| Pine | Vdu-based mail utility |
