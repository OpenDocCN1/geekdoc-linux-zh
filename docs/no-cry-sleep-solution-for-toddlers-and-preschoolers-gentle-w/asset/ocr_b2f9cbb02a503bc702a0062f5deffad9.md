# Linux Files

You can name a file using any letters, underscores, and numbers. You can also include periods and commas. Except in certain special cases, you should never begin a filename with a period. Other characters, such as slashes, question marks, or asterisks, are reserved for use as special characters by the system and should not be part of a filename. Filenames can be as long as 256 characters. Filenames can also include spaces, although to reference filenames from the command line, you need to be sure to encase them in quotes.

On a desktop like GNOME and KDE you do not need quotes.

You can include an extension as part of a filename. A period is used to distinguish the filename proper from the extension. Extensions can be useful for categorizing your files. You are probably familiar with certain standard extensions that have been adopted by convention. For example, C source code files always have an extension of .c. Files that contain compiled object code have a .o extension. You can, of course, make up your own file extensions. The following examples are valid Linux filenames. Keep in mind that to reference the last name on the command line you would have to encase it in quotes "New book review":

+   preface
+   chapter2
+   9700info
+   New_Revisions
+   calc.c
+   intro.bk1
+   intro.bk
+   New book review

Special initialization files are also used to hold shell configuration commands. These are the hidden, or dot, files, which begin with a period. Dot files used by commands and applications have predetermined names, such as the .mozilla directory used to hold your Mozilla data and configuration files. Recall that when you use ls to display your filenames, the dot files will not be displayed. To include the dot files, you need to use ls with the -a option. Dot files are discussed in more detail in the chapter on shell configuration, Chapter 9.

As shown in Figure 10-1, the ls -l command displays detailed information about a file. First the permissions are displayed, followed by the number of links, the owner of the file, the name of the group the user belongs to, the file size in bytes, the date and time the file was last modified, and the name of the file. Permissions are discussed in detail in the chapter later in this book.

![](bbox=[0.05, 0.93, 0.95, 0.99])

| File type | Number of links | Owner name | Group name | Size of file in bytes | Date and time last modified | File name |
|----------|---------------|------------|------------|----------------------|-----------------------------|----------|
|-rw-r--r-- | 1 | chris | weather | 207 | Feb 20 11:55 | mydata |

```
$ ls -l mydata
```

```
-rw-r--r-- 1 chris weather 207 Feb 20 11:55 mydata
```