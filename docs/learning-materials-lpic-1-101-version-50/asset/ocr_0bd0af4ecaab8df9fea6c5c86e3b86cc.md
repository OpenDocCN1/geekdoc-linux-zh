The preceding command would create three directories `dir1`, `dir2` and `dir3` at the same time.

To create a directory together with its subdirectories use the option `-p` ("parents"):

```
```
$ mkdir -p parents/children
```
```

This command would create the directory structure `parents/children`, i.e. it would create the directories `parents` and `children`. `children` would be located inside `parents`.

# ## Removing Directories with `rmdir`

`rmdir` deletes a directory *if it is empty*. Its syntax is given by:

```
```
rmdir OPTIONS DIRECTORY
```
```

where `DIRECTORY` could be a single argument or a list of arguments.

```
```
$ rmdir dir1
```
```

This command would delete `dir1`.

```
```
$ rmdir dir1 dir2
```
```

This command would simultaneously delete `dir1` and `dir2`.

You may remove a directory with its subdirectory:

```
```
$ rmdir -p parents/children
```
```

This would remove the directory structure `parents/children`. Note that if any of the directories are not empty, they will not be deleted.

# ## Recursive Manipulation of Files and Directories

To manipulate a directory and its contents, you need to apply *recursion*. Recursion means, do an action and repeat that action all down the directory tree. In Linux, the options `-r` or `-R` or `--recursive` are generally associated with recursion.