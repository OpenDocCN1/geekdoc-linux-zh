```
2    Pam  Meyer CS    3.61
3    Jim  DAVIS CS    2.71
4    Jason Kim  ECE    3.97
5    Amy  Nash ECE    2.38
%
```

Also, if you need to display files with a time stamp and page numbers, you can use the pr utility. It displays file contents as the cat command does, but it also partitions the file into pages and inserts a header for each page. The page header contains today's date, current time, file name, and page number. The pr command, like the cat command, can display multiple files, one after the other. The following session illustrates a simple use of the pr command.

```
% pr student_records
Aug 25 19:49 2014 student_records Page 1

Jonh Doe ECE 3.54
Pam Meyer CS 3.61
Jim DAVIS CS 2.71
Jason Kim ECE 3.97
Amy Nash ECE 2.38
<Blank lines until the end of page>
%
```

You can print files with line numbers and a page header by connecting the nl, pr, and lp (or lpr) commands. This method is discussed in Chapter 9.

# 6.2.2 Viewing Files One Page at a Time

If the file to be viewed is larger than one page, you can use the more command, also known as the UNIX pager, to display the file a screenful at a time. The following is a brief description of the command.

```
SYNTAX
more [options] [file-list]

Purpose: Concatenate/display the files in file-list on standard output a screenful at a time
Output: Contents of the files in file-list displayed on the screen, one page at a time
Commonly used options/features:
+/str  Start two lines before the first line containing str
-nN    Display N line per screen/page
+N     Start displaying the contents of the file at line number N
```

When run without file-list, the more command, like the cat command, takes input from the keyboard one line at a time and sends it to the display screen. If a file-list is given as an argument, the command displays the contents of the files in file-list one screen at a