
### dirs

```
dirs [ option ]
```

Displays the directories you have added to the *directory stack*, a list of remembered directory names. To add directories to the stack, use *pushd*. To remove directories from the stack, use *popd*.

### OPTIONS

| Use This Option | To Do This |
|---|---|
| +n | Display the name of the *n*th directory in the stack, starting from zero |
| –n | Display the name of the *n*th directory from the end of the list |
| -l | Display entries with absolute path names |

### file

```
file [ option ] filename
```

Displays the type of content (text, executable, or data) that a file contains. For some data files, this utility can provide detailed information, including the name of the utility that *created* the data.

### OPTIONS

| Use This Option | To Do This |
|---|---|
| -b | Display the results concisely, omitting the filenames |
| -t filename | Obtain the names of the files to be examined from the specified filename |
| -L | Follow symlinks to their targets |
| -M filename | Obtain a list of *magic numbers* (codes representing various data types) from the specified filename |
| -s | Read block or character special files |
| -v | Show the version number |
| -z | Process compressed files |

### find

```
find [ path_name ] [ option ] [ [ test ] [ action ] ]
```

In its simple form (find pattern), this command searches the current directory for files with names that match the specified shell pattern (see Chapter 3). If you specify a path name, find starts searching at the specified directory and searches all associated subdirectories if there are any. You can also perform a more advanced search by specifying a test and an action. The default test is —name, while the default action is —print (displays the name of the files that meet the specified test). When you specify tests that call for a numerical specification (n), you can type n+ to indicate n or more than n, -n to indicate n or less than n, or n to indicate exactly n. For example, find -ctime -1 searches for files that were changed one or fewer hours ago. When you specify a path name, you cannot specify the test using the command’s short form; you must use —text ‘filename.’

> *See also locate.*

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| **-daystart** | When used with the various time tests (-amin, -atime, -cmin, -ctime, -min, and -mtime), measure time from the start of the current day rather than 24 hours ago. |
| **-depth** | Process each directory’s contents before processing the directory itself. |
| **-follow** | Display the files to which symbolic links point rather than the links themselves. |
| **-help, - –help** | Display available options, tests, and actions. |
| **-maxdepth levels** | Specify the number of levels to descend down a directory tree from the current level. Use an integer (a whole number) other than zero to specify *levels*. |

| **Use This Option** | **To Do This** |
| --- | --- |
| --mindepth *levels* | Begin processing tests and actions at the specified level below the current directory. Use an integer (a whole number) other than zero to specify *levels*. |
| --mount, --xdev | Do not search directories on other mounted filesystems. |
| --noleaf | Use this option when searching non-Unix file-systems, such as CD-ROMs or MS-DOS disks. |
| --version, --version | Display the version number. |

### TESTS

| **Use This Test** | **To Do This** |
| --- | --- |
| --amin *n* | Match files that were last accessed *n*minutes ago |
| --anewer *filename* | Match files that have been accessed since the specified *filename* was modified |
| --atime *n* | Match files that were last accessed *n* hours ago |
| --cmin *n* | Match files that were last changed *n*minutes ago |
| --cnewer *filename* | Match files that have been changed since the specified *filename* was modified. |
| --ctime *n* | Match files that were last changed *n* hours ago |
| --empty | Match files with 0 bytes of content. |
| --fstype *type* | Match files stored on the specified type of filesystem, such as msdos or vfat. |
| --gid *n* | Match files owned by the numeric group ID specified by *n*. |
| --ilname *shell pattern* | Match symbolic links with the specified *shell pattern*. Enclose the *shell pattern* in quotation marks. This search ignores case. |
| –i\name *shell pattern* | Match files with the filename specified in shell pattern. Enclose the shell pattern in quotation marks. This search ignores case. |
| –i\name *shell pattern* | Match symbolic links with the specified shell pattern. Enclose the shell pattern in quotation marks. |
| –\name *shell pattern* | Match files with the filename specified in shell pattern. Enclose the shell pattern in quotation marks. This search is case sensitive. |
| –inum n | Match files with the specified inode number n. |
| –ipath *shell pattern* | Match the path with the specified shell pattern. Enclose the shell pattern in quotation marks. This search ignores case. |
| –iregex *regular expression* | Match the files with the filename specified in regular expression. This search ignores case. |
| –ilinks n | Match files that have n symbolic links. |
| –immin n | Match files that were last modified n minutes ago. |
| –imtime n | Match files that were last modified n hours ago. |
| –inewer *filename* | Match files that are newer than the file specified in filename. |
| –iowner | Match files that have no assigned owner. |
| –igroup | Match files that have no assigned group owner. |
| –ipath *shell pattern* | Match the path with the specified shell pattern. Enclose the shell pattern in quotation marks. |
| **-perm permissions** | Match files with the specified permissions (octal or symbolic). |
| **-regex regular expression** | Match the files with the filename specified in *regular expression*. |
| **-size n \| b \| c \| w** | Match files with the size specified by *n*. By default, *n* refers to the file size in 512-byte blocks (**-size nb**). You can also specify bytes (**-size nc**), kilobytes (**-size nk**), or 2-byte words (**-size nw**). |
| **-type \| b \| c \| d \| f \| l \| p \| s** | Match files of the specified type:<br>- **b** Buffered block.<br>- **c** Unbuffered character.<br>- **d** Directory.<br>- **f** Regular file (default).<br>- **l** Symbolic link.<br>- **p** Named pipe (FIFO).<br>- **s** socket. |
| **-uid n** | Match files belonging to the user whose numerical ID is specified by *n*. |
| **-used n** | Match files last accessed *n* days after any of its attributes were last changed. |
| **-user username** | Match files belonging to the user specified by *username*. |
| **-xtype \| b \| c \| d \| f \| l \| p \| s** | Match symbolic links of the specified type:<br>- **b** Buffered block.<br>- **c** Unbuffered character.<br>- **d** Directory.<br>- **f** Regular file (default).<br>- **l** Symbolic link.<br>- **p** Named pipe (FIFO).<br>- **s** Socket. |

### ACTIONS

| Use This Option | To Do This |
|---|---|
| -exec command‘’; | Run the utility specified by command. Use ‘’ to echo the filename specified in the test you are using. Use ‘;’ to terminate the command. Note that ‘’ and ‘;’ must be enclosed in single quotation marks so that the shell does not interpret them. |
| -fls filename | Write the contents of retrieved file(s) to the file specified by filename. |
| -fprint filename | Write the names of retrieved file(s) to the file specified by filename. |
| -ls | Display the names of retrieved file(s) using ls -dis. |
| -print | Display the names of retrieved file(s). This is the default action. |
| -print0 | Display the names of retrieved file(s) in a format that enables xargs to work with filenames containing spaces. |

### EXAMPLES

| This Command | Does the Following |
|---|---|
| find *.jpg | Finds all the files in the current directory with the .jpg extension. |
| find /home/suzanne -name \*.doc\* | Finds all the files in the specified directory (\ /home\ /suzanne) and all associated subdirectories that have the .doc extension. |
| find /home/suzanne -ctime -2 | Finds all the files in the specified directory (\ /home\ /suzanne) that have been changed within the past two hours. |
| find /home/suzanne -newer ‘essay1.doc’ . | Finds all the files in the specified directory (\ /home\ /suzanne) that are newer than essay1.doc |
