
# ls 745

The following command displays the names of all files in the current directory, including those that begin with a dot (.), which normally are not displayed.

```
$ ls -a
```

The following example provides information on all files, including those that begin with a dot (-a option), the i-number--the memory address of the inode associated with the file--printed in the left-hand column (the -i option); the size (in blocks) of the files, printed in the column to the right of the i-numbers (the -s option); finally, the report is displayed in the numeric version of the long list (-n option), printing the UID (of user name) and GID (of group name) numbers associated with the files.

```
$ ls -aisn
total 10272
297874 2 drwxr-xr-x 6 1001 10 512 Mar 9 13:50
296620 2 drwxr-xr-x 6 1001 1 512 Mar 3 18:49
297877 2 drwxr-r--x- 1 1001 10 411 Mar 19:05 .cshrc
407708 2 drwxr-xr-x 14 1001 10 512 Mar 9 13:15 .dt
297858 10 drwxr-xr-x 1 1001 10 5111 Mar 3 19:52 .dtprofile
41663 2 drwxr-xr-x 2 1001 10 512 Mar 4 07:42 .hotjava
81587 2 drwxr-rwx-x 2 1001 10 512 Mar 4 11:22 .jetamin
297890 2 drwxr-r--r- 1 1001 10 598 Mar 3 18:48 .sh_history
297884 2 drwxr------ 1 1001 10 512 Mar 6 16:52 .login
36679 2 drwx------ 1 1001 10 36 Mar 6 13:15 .solregis
297890 8 drwxr-r--r- 1 1001 10 100 Mar 9 13:15 .Xauthority
297880 8 drwxr-r--r- 1 1001 10 3985 Mar 4 12:55 .Kdaults
297885 0 drwx------ 1 1001 10 0 Mar 8 12:55 .a.out
297888 2 drwxr-r--r- 1 1001 10 783 Mar 8 18:08 bibliography
297881 240 drwx------ 1 1001 10 111560 Mar 5 10:33 core
297879 4 drwxr-r--r- 1 1001 10 1068 Mar 8 18:11 examples
297887 2 drwxr-r--r- 1 1001 10 265 Mar 8 18:00 kookaburra-1
297876 9984 drwx------ 1 1001 10 5097472 Mar 3 19:03 Sold515.pkg
```

When the sizes of files in a directory are listed, a total count of files, including indirect blocks, is printed.

The following scenario shows how you can list files that have unprintable or white space in their file names: when you want to delete a file that has embedded white space or control characters in the file name.

If a file has been created with characters or spaces in its name, the -b option to ls shows you exactly which characters are in the file name so that you can rename or delete it. For example, if you see the following in your listing:

```
$ ls
tfile
tfile: No such file or directory
```

and when you receive the following message when you try to remove the file, the file name probably contains invisible characters.

# 746

Then, you can use the -b option to display the real file-name characters, as shown in the following example.

```
$ ls -b tfile
test\010\010\010file
$'
```

In this case, the actual file name is

test [BACKSPACE] [BACKSPACE] [BACKSPACE] file
The backspaces are printed by the -b option as octal 010.
One way to remove the file, now that you know the actual characters in the file name, is shown below.

```
$ rm test*file
$
```

The following example enables you to get a helpful listing that indicates directories, symbolic links, sockets and executable files.

```
$ ls -F
..          .kshrc       .wastebasket/  export/     opt/      var/
../         .lsf_n      a/            platform/   vol/
.Tauthority  .netscape/    bin@         kernel/     prefs_v3/
.Xauthority  .profile     cdrom/      lib         proc/
.cpan        .rnd          db/         sbin/
.dt           .sh_history dev/          lastfound/ tftboot/
.dtprofile   .ssh/         devices/     mat         tmp/
.fm/           etc/         net/         usr/
```

Directories have /, symbolic links have @, and executables have *.

Environment Variables

See environ(5) for descriptions of the following variables that affect the execution of: LC_COLLATE, LC_TYPE, LC_TIME, LC_MESSAGE, PATH, and TZ.

COLUMNS Determine the preferred column width for writing text. If this variable contains a string representing a decimal integer, ls calculates how many columns to write based on the width provided. File names are not truncated to fit into multiple column output. The order of ls output is handled by the locale and can be overridden by LC_COLLATE. For example, if LC_COLLATE equals c, dots are displayed first, followed by names with uppercase letters, and then by names with lowercase letters. But, if LC_COLLATE equals en_US.ISO8859-1, then leading dots are also considered in the sort order.

# ls # 747

# Exit Status

- 0 All information was written successfully.
- 1 An error occurred.

# Files

- /etc/group Group IDs for ls -g.
- /etc/passwd User IDs for ls -o.
- /usr/share/lib/terminfo Terminal database.

# Attributes

See attributes(5) for descriptions of the following:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | gllibc |
| CSI | Enabled |
| Interface Stability | Stable |

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | gllibc |
| CSI | Enabled |
| Interface Stability | Standard |

# See Also

chmod(1), cp(1), setfacl(1), terminfo(4), attributes(5), environ(5), largefile(5), m4(5)

# m4 — Macro Processor

Synopsis
/usr/bin/m4 [-e] [-s] [-B int] [-H int] [-S int] [-T int] [-Dname=val]...[-U name]... [file...]

Description
m4 command is a macro processor front end for C, assembler, and other languages. Each of the argument files is processed in order; if there are no files or if a file is -, the standard input is read. The processed text is written to the standard output.

Macro Syntax
Macro calls have the form:
name(arg1, arg2,..., argm)

The () must immediately follow the name of the macro. If the name of a defined macro is not followed by (), it is considered to be a call of that macro with no arguments. Macro names consist of alphanumeric characters and underscore (_), where the first character is not a digit.
Leading unquoted blanks, Tabs, and newlines are ignored while arguments are collected. Left and right single quotes are used to quote strings. The value of a quoted string is the string stripped of the quotes.

# Macro Processing

When a macro name is recognized, its arguments are collected by a search for a matching right parenthesis. If fewer arguments are supplied than are in the macro definition, the trailing arguments are taken to be null. Macro evaluation proceeds normally during the collection of the arguments, and commas or right parentheses that happen to turn up the value of a nested call are as effective as those in the original input text. After argument collection, the value of the macro is pushed back onto the input stream and rescanned.

# Options

- e Operate interactively. Ignore interrupts, and # the output.
- s Enable line sync output for the C preprocessor (#line..).
- B int Change the size of the push-back and argument-collection buffers from the default of 4,096.
- H int Change the size of the symbol table hash array from the default of 199. The size should be prime.
- S int Change the size of the stack call from the default of 100 slots. Macros take three slots, and nonmacro arguments take one.
- T int Change the size of the token buffer from the default of 512 bytes.

To be effective, the above options before any file names and before any -D or -U options.

- D name={val} Define name to val or null in val's absence.
- U name Undefine name.

# Operands

- file A path of a text file to be processed. If you specify no file or if it is -, the standard input.

# Usage

The m4 command makes the following built-in macros available. You can redefine these macros, but if you do, you lose their original meaning. Macro values are null unless otherwise stated.

- changequote Change quote symbols to the first and second arguments. The symbols can be up to five characters long. changequote without arguments restores the original values (that is, '').

- changecom Change left and right comment markers from the default # newline. With no arguments, the comment mechanism is effectively disabled. With one argument, the left marker becomes the argument and the right marker becomes newline. With two arguments, both are affected. Comment markers can be up to five characters long.
