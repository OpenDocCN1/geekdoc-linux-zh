You used the cut, paste, and sort commands to extract information from files, combine the information, and then sort and merge the information in a new file.

# SUMMARY

+   UNIX supports regular files, directories, character special files, and block special files. Regular files contain user information. Directories are system files for maintaining the file system's structure. Character special files are related to serial input/output devices, such as printers. Block special files are related to devices, such as disks.

+   Files can be structured in several ways. UNIX stores data, such as letters, product records, or vendor reports, in flat ASCII files. File structures depend on the kind of data being stored. Three kinds of regular files are unstructured ASCII characters, records, and trees.

+   When performing commands, UNIX processes data—it receives input from the standard input device and then sends output to the standard output device. UNIX refers to the standard devices for input and output as stdin and stdout, respectively. By default, stdin is the keyboard and stdout is the monitor. Another standard device, stderr, refers to the error file that defaults to the monitor.

+   Output from a command may be redirected from stdout to a disk file. Input to a command may be redirected from stdin to a disk file. The error output of a command may be redirected from stderr to a disk file.

+   The touch command updates a file's time and date stamps and creates empty files.

+   When you manipulate files, you work with the files themselves as well as their content. You can use file manipulation commands to create, delete, copy, move, find, and display files.

+   The rmdir command removes a directory.

+   The cut command extracts specific columns or fields from a file. Select the fields you want to cut by specifying their positions and separator character, or you can cut by character positions, depending on the data's organization.

+   To combine two or more files, use the paste command. Where cat appends data to the end of the file, the paste command combines files line by line. You can also use paste to combine fields from two or more files.

+   Use the sort command to sort a file's contents alphabetically or numerically. UNIX displays the sorted file on the screen by default, but you can also specify that you want to store the sorted data in a particular file.

# REVIEW QUESTIONS

+   1. The UNIX file deletion command is \_\_\_\_\_\_\_\_\_\_\_.
 a. del
 b. remove
 c. rm
 d. kill

+   2. A regular file contains \_\_\_\_\_\_\_\_\_\_\_.
 a. a user program
 b. directories