+   - To remove all files in the current working directory that begin with a hyphen and have the text “out” somewhere else in their file name, type:
+     `$ rm -- --*out* [RET]`
+   - To concatenate all files whose names consist of an “a” character followed by two or more characters, type:
+     `$ cat a??* [RET]`

# 5.9 Listing Directory Tree Graphs

Tree
DEB: tree
RPM: tree
WWW: ftp://mama.indstate.edu/linux/tree/

Use tree to output an ASCII text tree graph of a given directory tree.

⇒ To output a tree graph of the current directory and all its subdirectories, type:

```
$ tree [RET]
.
|-- projects
|   |-- current
|   `-- old
|   |-- 1
|   `-- 2
`-- trip
    `-- schedule.txt

4 directories, 3 files
$
```

In the preceding example, a tree graph is drawn showing the current directory, which contains the two directories projects and trip; the projects directory in turn contains the directories current and old.

To output a tree graph of a specific directory tree, give the name of that directory tree as an argument.