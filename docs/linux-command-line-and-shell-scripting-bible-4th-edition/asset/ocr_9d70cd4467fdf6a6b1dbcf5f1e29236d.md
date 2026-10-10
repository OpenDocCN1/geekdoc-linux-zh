files.

Another way to tell that these linked files are separate physical files is by viewing their inode numbers. The inode number of a file or directory is a unique identification number that the kernel assigns to each object in the filesystem. To view a file or directory's inode number, add the -i parameter to the ls command:

```
$ ls -i *test_file
1415020 slink_test_file 1415523 test_file
$
```

The example shows that the test file's inode number is 1415523, whereas the slink_test_file inode number is different (it is 1415020). Thus, they are different files.

A hard link creates a separate virtual file that contains information about the original file and where to locate it. However, the two files are actually the same physical file. To create a hard link, again the original file must preexist, except that this time no parameter is needed on the ln command:

```
$ ls -l *test_one
-rw-rw-r---. 1 christine christine 0 Feb 29 17:26 test_one
$
$ ln test_one hlink_test_one
$
$ ls -li *test_one
1415016 -rw-rw-r---. 2 christine christine 0 Feb 29 17:26 hlink_test_one
1415016 -rw-rw-r---. 2 christine christine 0 Feb 29 17:26 test_one
$
```

In the preceding example, after creating the hard link file, we used the ls -li command to show both the inode numbers and a long listing for the *test_one . Notice that both files, which are hard-linked together, share the same inode number. This is because they are physically the same file. Their file size is exactly the same as well.

# NOTE