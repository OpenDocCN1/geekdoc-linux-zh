report directory contains three files comprising the three parts of a report. Also on the fifth level are two subdirectories, regular and contract, which further organizes the information in the payroll directory.

A higher level directory is frequently called a parent directory. For example, in Figure 2-1, the directories plans, report, and payroll all have chang as their parent directory.

A pathname specifies the location of a directory or a file within the file system. For example, when you want to change from working on File A in Directory X to File B in Directory Y, you enter the pathname to File B. The operating system then uses this pathname to search through the file system until it locates File B.

A pathname consists of a sequence of directory names separated by slashes (/) that ends with a directory name or a file name. The first element in a pathname specifies where the system is to begin searching, and the final element specifies the target of the search. The following pathname is based on Figure 2-1:

```
/user/chang/report/part3
```

The first slash (/) represents the root directory and indicates the starting place for the search. The remainder of the pathname indicates that the search is to go to the user directory, then to the chang directory, next to the report directory, and finally to the part3 file.

Whether you are changing your current directory, sending data to a file, or copying or moving a file from one place in your file system to another, you use pathnames to indicate the objects you want to manipulate.

A pathname that starts with a slash (/) (the symbol representing the root directory) is called a full pathname or an absolute pathname. You can also think of a full pathname as the complete name of a file or a directory. Regardless of where you are working in the file system, you can always find a file or a directory by specifying its full pathname.

The file system also lets you use relative pathnames. Relative pathnames do not begin with the / that represents the root directory because they are relative to the current directory.

You can specify a relative pathname in one of several ways:

+   - As the name of a file in the current directory.
+   - As a pathname that begins with the name of a directory one level below your current directory.
+   - As a pathname that begins with .. (dot dot, the relative pathname for the parent directory).