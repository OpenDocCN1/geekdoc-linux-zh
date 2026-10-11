![](bbox=[0.1, 0.14, 0.22, 0.2])

![](bbox=[0.26, 0.14, 0.8, 0.42])

Although `ls` by itself does not tell you exactly that files are linked to one another, using it with the `-i` option will. This option lists the inode number for each file and shows clearly that files are linked because they share the same number. If two files have the same inode number, they share the control structure and are linked to the same file. If you find that two files have different inode numbers, then they are completely different files.

The following example shows the syntax and output for the `-i` option:

```
$ ls -i file_1 file_2 file_3 file_4
4747 file_1    4747 file_2  5655 file_3  8327 file_4
```

All links to a file are of equal value. The operating system does not distinguish in what order links are created. If there is more than one hard link to a file, you can remove all but one and still be able to link through that one remaining link. The links shown in the preceding example are examples of hard links.

# More About Symbolic Links

When creating symbolic links, use `ln` with the `-s` option. This will create an indirect pointer to the file you want to link to. The syntax and output for creating a typical symbolic link is shown in the following example:

```
$ ln -s myfile /tempfile/s2
$ ls -l /myfile /tempfile/s2
```