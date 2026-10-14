# 9.5 Compressed Files

File compression is useful for storing or transferring large files. When you compress a file, you shrink it and save disk space. File compression uses an algorithm to change the data in the file; to use the data in a compressed file, you must first uncompress it to restore the original data (and original file size).

The following recipes explain how to compress and uncompress files.

+   9.5.1 Compressing a File
+   Making files smaller.
+   9.5.2 Decompressing a File
+   Making files bigger.

# 9.5.1 Compressing a File

Use the gzip ("GNU zip") tool to compress files. It takes as an argument the name of the file or files to be compressed; it writes a compressed version of the specified files, appends a `.gz` extension to their file names, and then deletes the original files.

+   To compress the file `war-and-peace`, type:

```
$ gzip war-and-peace RET
```

This command compresses the file `war-and-peace`, putting it in a new file named `war-and-peace.gz`; gzip then deletes the original file, `war-and-peace`.

# 9.5.2 Decompressing a File

To access the contents of a compressed file, use gunzip to decompress (or "uncompress") it.