```
cp -r dir1 dir2
```

Copy the contents of directory dir1 to directory dir2. If directory dir2 does not exist, it is created and, after the copy, will contain the same contents as directory dir1. If directory dir2 does exist, then directory dir1 (and its contents) will be copied into dir2.

# mv – Move And Rename Files

The mv command performs both file moving and file renaming, depending on how it is used. In either case, the original filename no longer exists after the operation. mv is used in much the same way as cp:

```
mv item1 item2
```

to move or rename file or directory "item1" to "item2" or:

```
mv item... directory
```

to move one or more items from one directory to another.

# Useful Options And Examples

mv shares many of the same options as cp:

Table 5-6: mv Options

| Option | Meaning |
|---|---|
| -i, --interactive | Before overwriting an existing file, prompt the user for confirmation. If this option is not specified, mv will silently overwrite files. |
| -u, --update | When moving files from one directory to another, only move files that either don't exist, or are newer than the existing corresponding files in the destination directory. |
| -v, --verbose | Display informative messages as the move is |