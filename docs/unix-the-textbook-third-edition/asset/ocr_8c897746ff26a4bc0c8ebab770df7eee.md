encouraged to read the online manual pages for the ls command on your system, or see the Command Appendix at the CRC Press website for this book for a detailed description of the command.

By using the shell metacharacters and regular expressions, you can specify a particular set of files and directories in the file system structure, or a particular set of strings in files or directories. For example, the following command can be used in the C shell to display the long lists for all the files in the ~/courses/ee446 directory that have the .c extension and start with the string lab followed by zero or more characters, with the condition that the first of these characters cannot be 5.

```
$ ls -l ~/courses/ee446/lab[^5]*.c
...
$
```

Similarly, the following command can be used to display the inode numbers and names of all the files in your current directory that have four-character names and an .html extension. The file names must start with a letter, followed by any two characters, and end with a digit from 1 through 5.

```
$ ls -i [a-zA-Z]??[1-5].html
...
$
```

The following command under the C shell displays the names of all the files in your home directory that do not start with a digit and that end with .c or .C. In other words, the command displays the names of all the C and C++ source program files that do not start with a digit. Under the Bourne shell, you may replace the ^ character with the ! character. Thus, the ls ~/[^0-9]*.[c,C] command would produce the same results.

```
$ ls ~/[ ^0-9]*.[c,C]
...
$
```

# 4.5.6 Determining the Type of a File's Contents

Because UNIX does not support file extensions, you can use any extension name for any file. This means that you can use the .jpg extension for an executable program file. Thus, you cannot determine the type of content of a file by simply looking at its name. Since many software tools require the use of extensions and the user may rely on extensions, extension names are, therefore, still significant. In UNIX, you can find the type of a file's contents by using the file command. Mostly, this command is used to determine whether a file contains text or binary data. Doing so is important because text files can be displayed on a terminal screen, whereas displaying the contents of a binary file shows "garbage" on your terminal screen and can also freeze your terminal, as it may interpret some of the binary values as control codes. The command has the following syntax.