
command displays the weather file in the parent directory. The pathname for the file is the .. symbol followed by a slash and the filename.

```
$ cat ../weather
raining and warm
```

Tip You can use the cd command with the .. symbol to step back through successive parent directories of the directory tree from a lower directory.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_234_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abchm.html

## File and Directory Operations: find, cp, mv, rm, and ln

As you create more and more files, you may want to back them up, change their names, erase some of them, or even give them added names. Linux provides you with several file commands that enable you to search for files, copy files, rename files, or remove files (see Table 10-5 later in this chapter). If you have a large number of files, you can also search them to locate a specific one. The commands are shortened forms of full words, consisting of only two characters. The cp command stands for "copy" and copies a file, mv stands for "move" and renames or moves a file, rm stands for "remove" and erases a file, and ln stands for "link" and adds another name for a file, often used as a shortcut to the original. One exception to the two-character rule is the find command, which performs searches of your filenames to find a file.

### Searching Directories: find

Once you have a large number of files in many different directories, you may need to search them to locate a specific file, or files, of a certain type. The find command enables you to perform such a search. The find command takes as its arguments directory names followed by several possible options that specify the type of search and the criteria for the search. find then searches within the directories listed and their subdirectories for files that meet these criteria. The find command can search for a file by name, type, owner, and even the time of the last update.

```
$ find directory-list -option criteria
```

The -name option has as its criteria a pattern and instructs find to search for the filename that matches that pattern. To search for a file by name, you use the find command with the directory name followed by the -name option and the name of the file.

```
$ find directory-list -name filename
```

The find command also has options that merely perform actions, such as outputting the results of a search. If you want find to display the filenames it has found, you simply include the -print option on the command line along with any other options. The -print option instructs find to output to the standard output the names of all the files it locates (you can also use the -ls option to list files in the long format). In the next example, the user searches for all the files in the reports directory with the name monday. Once located, the file, with its relative pathname, is printed.

```
$ find reports -name monday -print
```

The find command prints out the filenames using the directory name specified in the directory list. If you specify an absolute pathname, the absolute path of the found directories will be output. If you specify a relative pathname, only the relative pathname is output. In the preceding example, the user specified a relative pathname, reports, in the directory list. Located filenames were output beginning with this relative pathname. In the next example, the user specifies an absolute pathname in the directory list. Located filenames are then output using this absolute pathname.

```
$ find /home/chris -name monday -print
```

### Searching the Working Directory

If you want to search your working directory, you can use the dot in the directory pathname to represent your working directory. The double dots would represent the parent directory. The next example searches all files and subdirectories in the working directory, using the dot to represent the working directory. If you are located in your home directory, this is a convenient way to search through all your own directories. Notice the located filenames are output beginning with a dot.

```
$ find . -name weather -print
```

You can use shell wildcard characters as part of the pattern criteria for searching files. The special character must be quoted, however, to avoid evaluation by the shell. In the next example, all files with the .c extension in the programs directory are searched for:

```
$ find programs -name '*.c' -print
```

### Locating Directories

You can also use the find command to locate other directories. In Linux, a directory is officially classified as a special type of file. Although all files have a byte-stream format, some files, such as directories, are used in special ways. In this sense, a file can be said to have a file type. The find command has an option called -type that searches for a file of a given type. The -type option takes a one-character modifier that represents the file type. The modifier that represents a directory is a d. In the next example, both the directory name and the directory file type are used to search for the directory called thankyou:

```
$ find /home/chris -name thankyou -type d -print
/home/chris/letters/thankyou
$
```

File types are not so much different types of files as they are the file format applied to other components of the operating system, such as devices. In this sense, a device is treated as a type of file, and you can use find to search for devices and directories, as well as ordinary files. Table 10-4 lists the different types available for the find command's -type option.

Table 10-4: The find Command

| Command or Option | Execution |
|---|---|
| find | Searches directories for files according to search criteria. This command has several options that specify the type of criteria and actions to be taken. |
| -name pattern | Searches for files with the pattern in the name. |
| -group name | Searches for files belonging to this group name. |
| -size numc | Searches for files with the size num in blocks. If c is added after num, the size in bytes (characters) is searched for. |
| -mtime num | Searches for files last modified num days ago. |
| -newer pattern | Searches for files modified after the one matched by pattern. |
| -print | Outputs the result of the search to the standard output. The result is usually a list of filenames, including their full pathnames. |
| -type filetype | Searches for files with the specified file type. File type can be b for block device, c for character device, d for directory, f for file, or l for symbolic link. |

### Copying Files

To make a copy of a file, you simply give cp two filenames as its arguments (see Table 10-5). The first filename is the name of the file to be copied-the one that already exists. This is often referred to as the source file. The second filename is the name you want for the copy. This will be a new file containing a copy of all the data in the source file. This second argument is often referred to as the destination file. The syntax for the cp command follows:

```
$ cp source-file destination-file
```

In the next example, the user copies a file called proposal to a new file called oldprop:

```
$ cp proposal oldprop
```

You could unintentionally destroy another file with the cp command. The cp command generates a copy by first creating a file and then copying data into it. If another file has the same name as the destination file, that file is destroyed and a new file with that name is created. By default, Red Hat configures your system to check for an existing copy by the same name (cp aliases with the -i option, see Chapter 9). To copy a file from your working directory to another directory, you only need that directory name as the second argument in the cp command. In the next example, the proposal file is overwritten by the newprop file. The proposal file already exists.

```
$ cp newprop proposal
```

You can use any of the wildcard characters to generate a list of filenames to use with cp or mv. For example, suppose you need to copy all your C source code files to a given directory. Instead of listing each one individually on the command line, you could use an * character with the .c extension to match on and generate a list of C source code files (all files with a .c extension). In the next example, the user copies all source code files in the current directory to the sourcebks directory:

```
$ cp *.c sourcebks
```

If you want to copy all the files in a given directory to another directory, you could use * to match on and generate a list of all those files in a cp command. In the next example, the user copies all the files in the props directory to the oldprop directory. Notice the use of a props pathname preceding the * special characters. In this context, props is a pathname that will be appended before each file in the list that * generates.

```
$ cp props/* oldprop
```

You can, of course, use any of the other special characters, such as ., ?, or []. In the next example, the user copies both source code and object code files (.c and .o) to the projbk directory:

```
$ cp *.[oc] projbk
```

When you copy a file, you may want to give the copy a different name than the original. To do so, place the new filename after the directory name, separated by a slash.

```
$ cp filename directory-name/new-filename
```

### Moving Files

You can use the mv command either to rename a file or to move a file from one directory to another. When using mv to rename a file, you simply use the new filename as the second argument. The first argument is the current name of the file you are renaming. If you want to rename a file when you move it, you can specify the new name of the file after the directory name. In the next example, the proposal file is renamed with the name version1:

```
$ mv proposal version1
```

As with cp, it is easy for mv to erase a file accidentally. When renaming a file, you might accidentally choose a filename already used by another file. In this case, that other file will be erased. The mv command also has an -i option that checks first to see if a file by that name already exists.

You can also use any of the special characters described in Chapter 8 to generate a list of filenames to use with mv. In the next example, the user moves all source code files in the current directory to the newproj directory:

```
$ mv *.c newproj
```

If you want to move all the files in a given directory to another directory, you can use * to match on and generate a list of all those files. In the next example, the user moves all the files in the reports directory to the repbks directory:

```
$ mv reports/* repbks
```
