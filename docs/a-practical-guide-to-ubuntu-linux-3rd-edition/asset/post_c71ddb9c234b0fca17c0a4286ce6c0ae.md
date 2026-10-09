
## Page breaks for the printer

CONTROL-L tells the printer to skip to the top of the next page. You can enter this character anywhere in a document by pressing CONTROL-L while you are in Input mode. If `^L` does not appear, press CONTROL-V before CONTROL-L.

### ENDING THE EDITING SESSION

While you are editing, vim keeps the edited text in an area named the *Work buffer*. When you finish editing, you must write out the contents of the Work buffer to a disk file so that the edited text is saved and available when you next want it.

Make sure vim is in Command mode, and use the `ZZ` command (you must use uppercase *Zs*) to write your newly entered text to the disk and end the editing session. After you give the `ZZ` command, vim returns control to the shell. You can exit with `:q!` if you do not want to save your work.

**Do not confuse `ZZ` with `CONTROL-Z`**

When you exit from vim with `ZZ`, make sure that you type `ZZ` and not `CONTROL-Z` (typically the suspend key). When you press `CONTROL-Z`, vim disappears from your screen, almost as though you had exited from it. In fact, vim will continue running in the background with your work unsaved. Refer to “Job Control” on page 307. If you try to start editing the same file with a new vim command, vim displays a message about a swap file.

### THE COMPATIBLE PARAMETER

The **compatible** parameter makes vim more compatible with vi. By default this parameter is not set. From the command line use the `-C` option to set the **compatible** parameter and use the `:-N` option to unset it. To get started with vim you can ignore this parameter.

Setting the **compatible** parameter changes many aspects of how vim works. For example, when the **compatible** parameter is set, the Undo command (page 192) can undo only your most recent change; in contrast, with the **compatible** parameter unset, you can call Undo repeatedly to undo many changes. To obtain more details on the **compatible** parameter, give the command `:help compatible` RETURN. To display a complete list of vim’s differences from the original vi, use `:help vi-diff` RETURN. See page 190 for a discussion of the `help` command.

### CHAPTER SUMMARY

The utilities introduced in this chapter are a small but powerful subset of the many utilities available on an Ubuntu Linux system. Because you will use them frequently and because they are integral to the following chapters, it is important that you become comfortable using them.

The utilities listed in Table 5-2 manipulate, display, compare, and print files.

**Table 5-2** File utilities

| Utility | Function |
| :--- | :--- |
| cp | Copies one or more files (page 163) |
| diff | Displays the differences between two files (page 168) |
| file | Displays information about the contents of a file (page 170) |
| grep | Searches file(s) for a string (page 166) |
| head | Displays the lines at the beginning of a file (page 166) |
| lpq | Displays a list of jobs in the print queue (page 165) |
| lpr | Places file(s) in the print queue (page 165) |
| lprm | Removes a job from the print queue (page 165) |
| mv | Renames a file or moves file(s) to another directory (page 164) |
| sort | Puts a file in order by lines (page 168) |
| tail | Displays the lines at the end of a file (page 167) |
| uniq | Displays the contents of a file, skipping adjacent duplicate lines (page 168) |

To reduce the amount of disk space a file occupies, you can compress it with the **bzip2** utility. Compression works especially well on files that contain patterns, as do most text files, but reduces the size of almost all files. The inverse of **bzip2**—**bunzip2**—restores a file to its original, decompressed form. Table 5-3 lists utilities that compress and decompress files. The **bzip2** utility is the most efficient of these.

**Table 5-3** (De)compression utilities

| Utility | Function |
| :--- | :--- |
| bunzip2 | Returns a file compressed with **bzip2** to its original size and format (page 175) |
| bzcat | Displays a file compressed with **bzip2** (page 175) |
| bzip2 | Compresses a file (page 174) |
| compress | Compresses a file (not as well as **bzip2** or **gzip**; page 176) |
| gunzip | Returns a file compressed with **gzip** or **compress** to its original size and format (page 175) |
| gzip | Compresses a file (not as well as **bzip2**; page 175) |
| zcat | Displays a file compressed with **gzip** (page 175) |

An archive is a file, frequently compressed, that contains a group of files. The **tar** utility (Table 5-4) packs and unpacks archives. The filename extensions **_tar.bz2**, .tar.gz, and .tgz identify compressed tar archive files and are often seen on software packages obtained over the Internet.

**Table 5-4** Archive utility

| Utility | Function |
| :--- | :--- |
| tar | Creates or extracts files from an archive file (page 176) |

The utilities listed in Table 5-5 determine the location of a utility on the local system. For example, they can display the pathname of a utility or a list of C++ compilers available on the local system.

**Table 5-5** Location utilities

| Utility | Function |
| :--- | :--- |
| mlocate | Searches for files on the local system (page 180) |
| whereis | Displays the full pathnames of a utility, source code, or man page (page 178) |
| which | Displays the full pathname of a command you can run (page 178) |

Table 5-6 lists utilities that display information about other users. You can easily learn a user's full name, the user's login status, the login shell of the user, and other items of information maintained by the system.

**Table 5-6** User and system information utilities

| Utility | Function |
| :--- | :--- |
| finger | Displays detailed information about users, including their full names (page 181) |
| hostname | Displays the name of the local system (page 163) |
| w | Displays detailed information about users who are logged in on the local system (page 183) |
| who | Displays information about users who are logged in on the local system (page 180) |

The utilities shown in Table 5-7 can help you stay in touch with other users on the local network.

**Table 5-7** User communication utilities

| Utility | Function |
| :--- | :--- |
| mesg | Permits or denies messages sent by write (page 185) |
| write | Sends a message to another user who is logged in (page 184) |

Table 5-8 lists miscellaneous utilities.

| Utility | Function |
| :--- | :--- |
| date | Displays the current date and time (page 172) |
| echo | Copies its arguments (page 135) to the screen (page 171) |
| vim | Edits text (page 186) |

### EXERCISES

- Which commands can you use to determine who is logged in on a specific terminal?

- How can you keep other users from using `write` to communicate with you? Why would you want to?

- What happens when you give the following commands if the file named `done` already exists?

```
$ cp to_do done
$ mv to_do done
```

- How can you find out which utilities are available on your system for editing files? Which utilities are available for editing on your system?

- How can you find the phone number for Ace Electronics in a file named `phone` that contains a list of names and phone numbers? Which command can you use to display the entire file in alphabetical order? How can you display the file without any adjacent duplicate lines? How can you display the file without any duplicate lines?

- What happens when you use `diff` to compare two binary files that are not identical? (You can use `gzip` to create the binary files.) Explain why the `diff` output for binary files is different from the `diff` output for ASCII files.

- Create a `.plan` file in your home directory. Does `finger` display the contents of your `.plan` file?

- What is the result of giving the `which` utility the name of a command that resides in a directory that is not in your search path?

- Are any of the utilities discussed in this chapter located in more than one directory on the local system? If so, which ones?

- Experiment by calling the `file` utility with the names of files in `/usr/bin`. How many different types of files are there?
