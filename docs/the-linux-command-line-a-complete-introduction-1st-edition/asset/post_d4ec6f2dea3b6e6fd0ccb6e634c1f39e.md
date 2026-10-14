
## 4 MANIPULATING FILES AND DIRECTORIES

At this point, we are ready for some real work! This chapter will introduce the following commands:

- cp—Copy files and directories.
- mv—Move/rename files and directories.
- mkdir—Create directories.
- rm—Remove files and directories.
- ln—Create hard and symbolic links.

These five commands are among the most frequently used Linux commands. They are used for manipulating both files and directories.

Now, to be frank, some of the tasks performed by these commands are more easily done with a graphical file manager. With a file manager, we can drag and drop a file from one directory to another, cut and paste files, delete files, and so on. So why use these old command-line programs?

The answer is power and flexibility. While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command-line programs. For example, how could we copy all the HTML files from one directory to another—but only those that do not exist in the destination directory or are newer than the versions in the destination directory? Pretty hard with a file manager. Pretty easy with the command line:

```
cp -u *.html destination
```

### Wildcards

Before we begin using our commands, we need to talk about the shell feature that makes these commands so powerful. Because the shell uses filenames so much, it provides special characters to help you rapidly specify groups of filenames. These special characters are called wildcards. Using wildcards (also known as globbing) allows you to select filenames based on patterns of characters. Table 4-1 lists the wildcards and what they select.

**Table 4-1: Wildcards**

| Wildcard | Matches |
|---|---|
| `*` | Any characters |
| `?` | Any single character |
| `[characters]` | Any character that is a member of the set characters |
| `[!characters]` | Any character that is not a member of the set characters |
| `[[:class:]]` | Any character that is a member of the specified class |

Table 4-2 lists the most commonly used character classes.

**Table 4-2: Commonly Used Character Classes**

| Character Class | Matches |
|---|---|
| `[:alnum:]` | Any alphanumeric character |
| `[:alpha:]` | Any alphabetic character |
| `[:digit:]` | Any numeral |
| `[:lower:]` | Any lowercase letter |
| `[:upper:]` | Any uppercase letter |

Using wildcards makes it possible to construct very sophisticated selection criteria for filenames. Table 4-3 lists some examples of patterns and what they match.

**Table 4-3: Wildcard Examples**

| Pattern | Matches |
|---|---|
| `*` | All files |
| `g*` | Any file beginning with g |
| `b*.txt` | Any file beginning with b followed by any characters and ending with .txt |
| `Data???` | Any file beginning with Data followed by exactly three characters |
| `[abc]*` | Any file beginning with either a, b, or c |
| `BACKUP.[0-9][0-9][0-9]` | Any file beginning with BACKUP followed by exactly three numerals |
| `[[:upper:]]*` | Any file beginning with an uppercase letter |
| `[[:digit:]]*` | Any file beginning with a numeral |
| `*[[:lower:][:digit:]]` | Any file ending with a lowercase letter or the numerals 1, 2, or 3 |

Wildcards can be used with any command that accepts filenames as arguments, but we’ll talk more about that in Chapter 7.

### CHARACTER RANGES

If you are coming from another Unix-like environment or have been reading some other books on this subject, you may have encountered the [a-Z] or the [a-z] character range notations. These are traditional Unix notations and worked in older versions of Linux as well. They can still work, but you have to be very careful with them because they will not produce the expected results unless properly configured. For now, you should avoid using them and use character classes instead.

### WILDCARDS WORK IN THE GUI TOO

Wildcards are especially valuable, not only because they are used so frequently on the command line but also because they are supported by some graphical file managers.

- In Nautilus (the file manager for GNOME), you can select files using Edit ▸ Select Pattern. Just enter a file selection pattern with wildcards, and the files in the currently viewed directory will be highlighted for selection.
- In some versions of Dolphin and Konqueror (the file managers for KDE), you can enter wildcards directly on the location bar. For example, if you want to see all the files starting with a lowercase u in the /usr/bin directory, enter `/usr/bin/u*` in the location bar, and it will display the result.

Many ideas originally found in the command line interface make their way into the graphical interface, too. It is one of the many things that make the Linux desktop so powerful.

### mkdir—Create Directories

The mkdir command is used to create directories. It works like this:

```
mkdir directory...
```

A note on notation: In this book, when three periods follow an argument in the description of a command (as above), it means that the argument can be repeated; thus, in this case,

```
mkdir dir1
```

would create a single directory named dir1, while

```
mkdir dir1 dir2 dir3
```

would create three directories named dir1, dir2, and dir3.

### cp—Copy Files and Directories

The cp command copies files or directories. It can be used two different ways:

```
cp item1 item2
```

to copy the single file or directory item1 to file or directory item2 and:

```
cp item... directory
```

to copy multiple items (either files or directories) into a directory.
