+   3. What is the command to list *all* files (including hidden ones) by reverse modification time, in long form?

# ## 2.3 Renaming, copying, deleting

Next to listing files, probably the most common file operations involve renaming, copying, and deleting them. As with listing files, most modern operating systems provide a graphical user interface to such tasks, but in many contexts it is more convenient to perform them at the command line.

The way to rename a file is with the **mv** command, short for “move”:

```
`$ echo "test text" > test`
`$ mv test test_file.txt`
`$ ls`
test_file.txt
```

This renames the file called **test** to **test_file.txt**. The final step in the example runs `ls` to confirm that the file renaming was successful, but system-specific files other than the test file are omitted from the output shown. (The name “move” comes from the general use of `mv` to move a file to a different directory (Section 4), possibly renaming it en route. When the origin and target directories coincide, such a “move” reduces to a simple renaming.)

The way to copy a file is with **cp**, short for “copy”:

```
`$ cp test_file.txt second_test.txt`
`$ ls`
second_test.txt
test_file.txt
```

Finally, the command for deleting a file is **rm**, for “remove”:

```
`$ rm second_test.txt`
remove second_test.txt? y
`$ ls second_test.txt`
ls: second_test.txt: No such file or directory
```