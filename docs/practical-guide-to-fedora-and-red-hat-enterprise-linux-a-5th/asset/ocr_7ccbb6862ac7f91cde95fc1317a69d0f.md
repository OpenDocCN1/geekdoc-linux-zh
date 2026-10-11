The utilities listed in Table 5-2 manipulate, display, compare, and print files.

# **Table 5-2**
File utilities

| Utility | Function |
| :--- | :--- |
| cp | Copies one or more files (page 151) |
| diff | Displays the differences between two files (page 157) |
| file | Displays information about the contents of a file (page 157) |
| grep | Searches file(s) for a string (page 153) |
| head | Displays the lines at the beginning of a file (page 154) |
| lq | Displays a list of jobs in the print queue (page 153) |
| lpr | Places file(s) in the print queue (page 153) |
| lprme | Removes a job from the print queue (page 153) |
| mv | Renames a file or moves file(s) to another directory (page 152) |
| sort | Puts a file in order by lines (page 155) |
| tail | Displays the lines at the end of a file (page 154) |
| uniq | Displays the contents of a file, skipping successive duplicate lines (page 156) |

To reduce the amount of disk space a file occupies, you can compress it with the bzip2 utility. Compression works especially well on files that contain patterns, as do most text files, but reduces the size of almost all files. The inverse of bzip2—bunzip2—restores a file to its original, decompressed form. Table 5-3 lists utilities that compress and decompress files. The bzip2 utility is the most efficient of these.

# **Table 5-3**
(De)compression utilities

| Utility | Function |
| :--- | :--- |
| bunzip2 | Returns a file compressed with bzip2 to its original size and format (page 162) |
| bzcat | Displays a file compressed with bzip2 (page 162) |
| bzip2 | Compresses a file (page 162) |
| compress | Compresses a file (not as well as gzip) (page 163) |
| gunzip | Returns a file compressed with gzip or compress to its original size and format (page 163) |
| gzip | Compresses a file (page 163) |
| zcat | Displays a file compressed with gzip (page 163) |