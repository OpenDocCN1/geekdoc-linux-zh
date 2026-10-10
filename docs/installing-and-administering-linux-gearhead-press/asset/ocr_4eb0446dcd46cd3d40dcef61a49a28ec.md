rename test1 to the more appropriate name, bravery. Freston tells Don Quixote that had the Don realized beforehand that he would eventually rename test1, he could have done both at once (in other words, move the file and rename it) by using the same mv command. Here is how Freston tells the Don that it should have been done to begin with:

```
$ mv /mobile/test1 /admin/bravery<Enter>
```

# Deleting Files and Directories: The rm Command

The rm command removes the entries for the specified file(s) from a directory. But you must have the required permissions to remove the files. Here is the syntax for the rm command:

```
$ rm [-i] filename1 filename2 ...<Enter>
```

The -i option is the interactive version of the rm command. You do not receive confirmation after the files are removed. Example 5.8 shows the rm command with and without the -i option.

You can also remove directories with the rm command. The syntax is similar:

```
$ rm [-i] [-r] directoryname1 directoryname2 ...<Enter>
```

You can also use the -r option for recursive removal of directories and their respective files.

> **WARNING** Be careful when using the rm command with the -r option; that is, to remove directories and their contents recursively. Removal in this manner does not require the directories to be empty before execution.

In Example 4.9 in Chapter 4, we briefly mention the effects of the rm command on files with links. You might want to refer back to that example now in light of the discussion here.