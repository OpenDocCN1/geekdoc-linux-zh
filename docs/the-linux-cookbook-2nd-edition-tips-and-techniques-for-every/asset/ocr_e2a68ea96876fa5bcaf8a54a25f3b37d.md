NOTES: Renaming multiple files at once is a common request.

# 5.6 Removing Files and Directories

Use rm ("remove") to delete a file and remove it from the system. Give the name of the file to remove as an argument.

⇒ To remove the file notes in the current working directory, type:

```
$ rm notes RET
```

To remove a directory and all of the files and subdirectories it contains, use the -R ("recursive") option.

⇒ To remove the directory waste and all of its contents, type:

```
$ rm -R waste RET
```

To remove an empty directory, use rmdir; it removes the empty directories you specify. If you specify a directory that contains files or subdirectories, rmdir reports an error.

⇒ To remove the directory empty, type:

```
$ rmdir empty RET
```

# 5.6.1 Removing a File with a Strange Name

Files with strange characters in their names (such as white space, control characters, and beginning hyphens) pose a problem when you want to remove them. There are a few solutions to this problem.

# METHOD #1

One way is to use tab completion to complete the name of the file (see Recipe 3.1.4 [Letting the Shell Complete What You Type], page 61). This works when the name of the file you want to remove has enough characters to uniquely identify it so that completion can work.

⇒ To use tab completion to remove the file No Way in the current directory, type:

```
$ rm No TAB Way RET
```

In this example, once TAB was typed, the shell filled in the rest of the file name ("Way").