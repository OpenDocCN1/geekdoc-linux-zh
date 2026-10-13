+   .FBCIndex
+   .FBCLockFolder/
+   .ssh/
+   Desktop/
+   Documents/
+   Downloads/
+   Icon?
+   Library/
+   Movies/
+   Music/
+   Pictures/
+   Public/
+   Sites/
+   Temporary Items/

# File Contents

In the last section we looked at listing files and directories with the ls command. In this section we will look at the cat and wc commands. The cat command lets you view the contents of a file. The wc command gives you information about the number of words and lines in a file.

# cat

To view the contents of a file, we can use the cat (short for concatenate) command as follows

```
cat [opts] file1 ... fileN
```

Here opts are one or more of the options understood by cat, and file1...fileN are the names of the files whose contents should be printed. The options, opts, are optional and can be omitted. Two commonly used options are discussed later in this section.

The following example illustrates the use of cat:

```
$ cat fruits
```

This command prints the contents of a file called fruits:

| Fruit | Price/lbs | Quantity |
|---|---|---|
| Banana | $0.89 | 100 |
| Peach | $0.79 | 65 |
| Kiwi | $1.50 | 22 |
| Pineapple | $1.29 | 35 |
| Apple | $0.99 | 78 |