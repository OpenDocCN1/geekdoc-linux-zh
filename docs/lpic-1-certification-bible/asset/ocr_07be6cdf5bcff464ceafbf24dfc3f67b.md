# ### Using the compress utility

The compress utility is one of the first utilities for compressing files. Files compressed with this utility end in .Z. The original file is replaced by the compressed version. To compress a file use the following syntax:

```
compress filename
```

To uncompress the file use the following syntax:

```
uncompress filename.Z
```

With the ability of tar to compress an archive file when it is created, compress is rarely used.

# ### Using the gzip utility

The gzip utility is used to compress files. As you saw earlier, tar has the ability to do this automatically when creating an archive file. The command can also be run separately to compress any file. When a file is created using gzip, the original file is replaced by a new file with the same name and a .gz extension. The new file is created with the same permissions of the original file. Parameters for this command are listed in Table 11-12.

**Table 11-12** 
**Options Used with gzip**

| Option | Meaning |
| :--- | :--- |
| -c | Specifies that files be concatenated before compression, which allows for better compression. |
| -d | Decompresses the file. |
| -f | Forces compression and decompression of files. |
| -h | Displays the help information for the gzip utility. |
| -l | Lists all compression and file information for compressed files. |
| -r | Recursively searches directories for files to compress or uncompress depending on the options specified. |
| -t | Tests the files' integrity. |
| -v | Verbosely lists files as they are compressed or uncompressed. |

![](bbox=[0.12, 0.86, 0.2, 0.93])

While most people use gunzip to decompress a file, remember for the exam that you can also use gzip -d.