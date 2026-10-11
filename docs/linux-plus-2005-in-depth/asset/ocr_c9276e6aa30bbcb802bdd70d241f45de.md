# Table 12-2 Common options used with the *gzip* utility (Continued)

| Option | Description |
| --- | --- |
| -fast | Results in a lower compression ratio; same as the -1 option. |
| -h | Displays the syntax and available options for the *gzip* and *gunzip* commands. |
| -help |
| -l | Lists the compression ratio for files that have been compressed with *gzip*. |
| -list |
| -n | Does not allow *gzip* and *gunzip* to preserve the original modification and access time for files. |
| -no-name |
| -q | Suppresses all warning messages. |
| -quiet |
| -r | Specifies to compress or decompress all files recursively within a specified directory. |
| -recursive |
| -S *.suffix* | Specifies a file suffix other than *.gz* when compressing or decompressing files. |
| -suffix *.suffix* |
| -t | Performs a test decompression such that a user can view any error messages before decompression, when used with the *gunzip* command; it does not decompress files. |
| -test |
| -v | Displays verbose output (compression ratio and filenames) during compression and decompression. |
| -verbose |

# The *bzip2* utility

The **bzip2** utility differs from the **compress** and **gzip** utilities previously discussed in that it uses the **Burrows-Wheeler Block Sorting Huffman Coding** algorithm when compressing files. In addition, the **bzip2** utility cannot be used to compress a directory full of files, the **zcat** and **zmore** commands cannot be used to view files compressed with **bzip2**, and the compression ratio is **50-75%** on average.

Like the **compress** and **gzip** utilities, symbolic links are only compressed if the **-f** option is used, and the **-v** option can be used to display compression ratios. Also, file ownership, modification, and access time are preserved during compression.

The filename extension given to files compressed with **bzip2** is **.bz2**. To compress the samplefile and samplefile2 files and view their compression ratio and filenames, you can use the following commands: