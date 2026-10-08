# Task 7.1: Using file to Identify File Types

One of the most undervalued commands in UNIX is file, which is often neglected and collecting dust in some corner of the system. The file command is a program that can easily offer you a good hint as to the contents of a file by looking at the first few lines.

Unfortunately, there is a problem with the file command: It's not 100 percent accurate. The program relies on a combination of the permissions of a file, the filename, and an analysis of the first few lines of the text. If you had a file that started looking out like a C program or had executed permission enabled, file might well identify it as an executable program rather than an English text file.

![](bbox=[0.167, 0.345, 0.263, 0.417])

You can determine how accurate your version of file is by checking the size of database file types. You can do this with the UNIX command wc -l /etc/*. The number of entries in the database should be around 100. If you have many less than this number, you're probably going to have trouble. If you have considered more, you might have a very accurate version of file at your fingertips! Remember, however, even if it's relatively small, file can still offer invaluable suggestions regarding file content anyway.

+   1. Start logging in to your account and using the ls command to find a file or two to check.

```
% ls -F
Archives/
Info/old/
OWL/ PubAccessLists.Z rumors.260ct.Z
LISTS/ bin/ rumors.5Nov.Z
Mail/ educ src/\News/ mailing.bitnet.Z
```

Next, simply enter the file command, listing each of the files you'd like to analyze:

```
% file LISTS rumors.260ct.Z src
LISTS: ascii text
educ: ascii text
rumors.260ct.Z: block compressed 16 bit code data
src: directory
```

From this example, you can see that file correctly identifies src as a directory, offers considerable information on the compressed file rumors.260ct.Z, and tags both LISTS and educ as plain ASCII text files.

![](bbox=[0.067, 0.883, 0.138, 0.973])