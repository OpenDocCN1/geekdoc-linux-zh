If you want to copy all the files in a given directory to another directory, you could use \* to match on and generate a list of all those files in a cp command. In the next example, the user copies all the files in the props directory to the oldprop directory. Notice the use of a props pathname preceding the \* special character. In this context, props is a pathname that will be appended before each file in the list that \* generates.

```
$ cp props/* oldprop
```

You can, of course, use any of the other special characters, such as . , ? , or [ ]. In the next example, the user copies both source code and object code files (.c and .o) to the projbk directory:

```
$ cp *.[oc] projbk
```

When you copy a file, you may want to give the copy a different name than the original. To do so, place the new filename after the directory name, separated by a slash.

```
$ cp filename directory-name/new-filename
```

# Moving Files

You can use the mv command either to rename a file or to move a file from one directory to another. When using mv to rename a file, you simply use the new filename as the second argument. The first argument is the current name of the file you are renaming. If you want to rename a file when you move it, you can specify the new name of the file after the directory name. In the next example, the proposal file is renamed with the name version1:

```
$ mv proposal version1
```

As with cp, it is easy for mv to erase a file accidentally. When renaming a file, you might accidentally choose a filename already used by another file. In this case, that other file will be erased. The mv command also has an -i option that checks first to see if a file by that name already exists.

You can also use any of the special characters described in Chapter 8 to generate a list of filenames to use with mv. In the next example, the user moves all source code files in the current directory to the newproj directory:

```
$ mv *.c newproj
```

If you want to move all the files in a given directory to another directory, you can use \* to match on and generate a list of all those files. In the next example, the user moves all the files in the reports directory to the repbks directory:

```
$ mv reports/* repbks
```

> **NOTE** *The easiest way to copy files to a CD-R/RW or DVD-R/RW disc is to use the built-in* *Nautilus burning capability. Just insert a blank disk, open it as a folder, and drag and drop files* *to it. You will be prompted automatically to burn the files. You can also use any number of* *CD/DVD burning tools, such as K3B (see Chapter 3).*