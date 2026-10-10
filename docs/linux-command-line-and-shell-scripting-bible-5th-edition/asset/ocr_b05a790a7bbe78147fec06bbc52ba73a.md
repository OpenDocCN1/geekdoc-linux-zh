TABLE 4.7 **Linux File Compression Utilities**

| Utility | File Extension | Description |
|---|---|---|
| bzip2 | .bz2 | Uses the Burrows–Wheeler block sorting text compression algorithm and Huffman coding |
| compress | .Z | Original UNIX compress utility; starting to fade away into obscurity |
| gzip | .gz | The GNU Project’s compression utility; uses Lempel–Ziv–Welch coding |
| xz | .xz | A general-purpose compression utility gaining in popularity |
| zip | .zip | The UNIX version of the PKZIP program for Windows |
| 7-zip | .7z | Known for its high compression rate (2%–10% better than zip) |

The gzip package is a creation of the GNU Project in their attempt to create a free version of the original UNIX compress utility. This package includes these files:

+   ■ gzip for compressing files
+   ■ gcat for displaying the contents of compressed text files
+   ■ gunzip for uncompressing files

These utilities work the same way as the bzip2 utilities:

```
$ gzip myprog
$ ls -l my*
-rwxrwxr-x 1 rich rich 2197 2007-09-13 11:29 myprog.gz
$
```

The gzip command compresses the file you specify on the command line. You can also specify more than one filename or even use wildcard characters to compress multiple files at once:

```
$ gzip my*
$ ls -l my*
-rwxr-xr- 1 rich rich 103 Sep 6 13:43 myprog.c.gz
-rwxrwx-x 1 rich rich 5178 Sep 6 13:43 myprog.gz
-rwxr-xr- 1 rich rich 59 Sep 6 13:46 myscript.gz
-rwxr-xr- 1 rich rich 60 Sep 6 13:44 myscript2.gz
$
```

The gzip command compresses every file in the directory that matches the wildcard pattern.

# Archiving data

Although the zip command works great for compressing and archiving data into a single file, it’s not the standard utility used in the UNIX and Linux worlds. By far the most popular archiving tool used in UNIX and Linux is the tar command.