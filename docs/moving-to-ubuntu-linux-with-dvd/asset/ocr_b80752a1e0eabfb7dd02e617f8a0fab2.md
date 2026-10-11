Removing a directory can be a bit more challenging. The command `rmdir` seems simple enough. In fact, removing this directory was no problem:

```
$ rmdir trivia_dir
```

Removing this one, however, gave me an error:

```
$ rmdir junk_dir
rmdir: junk_dir: Directory not empty
```

You can only use `rmdir` to remove an empty directory. There is a –p option (as in *parents*) that enables you to remove a directory structure. For instance, you could remove a couple of levels like this:

```
rmdir –p junk_dir/level1/level2/level3
```

> **Warning** Beware of the `rm -rf *` command. Better yet, never use it. If you must delete an entire directory structure, change the directory to the one above it and explicitly remove the directory. This is also the first and best reason to do as much of your work as possible as a normal user and not root. Because root is all powerful, it is quite capable of completely destroying your system. Imagine that you are in the top-level directory ( / ) instead of /home/myname/junkdir when you initiate that recursive delete. It is far too easy to make this kind of mistake. *Beware.*

All the directories from `junk_dir` on down are removed, but *only* if they are empty of files. A better approach is to use the `rm` command with the -r, or *recursive*, option. Unless you are deleting only a couple of files or directories, you want to use the –f option as well.

```
$ rm -rf junk_dir
```