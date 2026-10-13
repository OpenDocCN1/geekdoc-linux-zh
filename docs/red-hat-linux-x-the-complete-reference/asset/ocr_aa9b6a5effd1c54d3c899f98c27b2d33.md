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

If you want to move all the files in a given directory to another directory, you can use * to match on and generate a list of all those files. In the next example, the user moves all the files in the reports directory to the repbks directory:

```
$ mv reports/* repbks
```