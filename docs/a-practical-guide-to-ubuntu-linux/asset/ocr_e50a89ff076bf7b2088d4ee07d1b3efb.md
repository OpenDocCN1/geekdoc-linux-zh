# COMPRESSING AND ARCHIVING FILES

Large files use a lot of disk space and take longer than smaller files to transfer from one system to another over a network. If you do not need to look at the contents of a large file, you may want to save it on a CD, DVD, or another medium and remove it from the hard disk. If you have a continuing need for the file, retrieving a copy from another medium may be inconvenient. To reduce the amount of disk you use without removing the file entirely, you can compress the file without losing any of the information it holds. Similarly a single archive of several files packed into a larger file is easier to manipulate, upload, download, and email than multiple files. You may frequently download compressed, archived files from the Internet. The utilities described in this section compress and decompress files and pack and unpack archives.

# bzip2: COMPRESSES A FILE

The bzip2 utility compresses a file by analyzing and recoding it more. The new version of the file looks completely different. In fact, the new file contains many nonprinting characters, you cannot view it. The bzip2 utility works practically well on files that contain a lot of repeated information, such as text and image data, although most data is already in a compressed format.

The following example shows a boring file. Each of the 8,000 lines of the file contains 72 e and a NEWLINE character that marks the end of the line. The file occupies more than half a megabyte of disk storage.

```
$ ls -l
-rw-r-- 1 sam 584000 2010-03-01 22:31 letter_e
```

The -l (long) option is ls to display more information about a file. Here it shows that letter_e is 584000 bytes. The -v (verbose) option shows bzip2 to report how you might be able to reduce the size of the file. In this case, shrink the file by 99.99 percent.

```
$ bzip2 -v letter_e
letter_e: 11680.0:1, 0.001 bytes/byte, 99.99% saved, 584000 in, 50 out.
$ ls -l
-rw-r-- 1 sam 50000 2010-03-01 22:31 letter_e.bz
```

Now the file is only 50 bytes long. The bzip2 utility also renames the file, adding bzip2 to its name. This naming convention reminds you that the file is compressed; you would not want to display or print it, for example, without decompressing it. The bzip2 utility does not change the modification date associated with the file, even though it completely changes the file's contents.

# Keep the original file by using the -k option

The bzip2 utility (and its counterpart, bunzip2) remove the original file when they compress or decompress a file. Use the -k (keep) option to keep the original file.