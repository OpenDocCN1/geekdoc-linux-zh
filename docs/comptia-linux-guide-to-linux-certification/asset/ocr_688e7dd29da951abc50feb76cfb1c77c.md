| Option | Description |
| :--- | :--- |
| -# | Specifies how thorough the compression will be, where # can be the number 1\~9. The option -1 represents fast compression, which takes less time to compress but results in a lower compression ratio. The option -9 represents thorough compression, which takes more time but results in a higher compression ratio. |
| -\-best | Results in a higher compression ratio; same as the -9 option. |
| -C<br>-\-stdout<br>-\-to-stdout | Displays the contents of the compress file to Standard Output (same function as the zcat command) when used with the gunzip command. |
| -d<br>-\-decompress<br>-\-uncompress | Decompresses the files specified (same as the gunzip command) when used with the gzip command. |
| -f<br>-\-force | Compresses symbolic links when used with the gzip command. When used with the gunzip command, it overwrites any existing files without prompting the user. |
| -\-fast | Results in lower compression ratio; same as the -1 option. |
| -h<br>-\-help | Displays the syntax and available options for the gzip and gunzip commands. |
| -l<br>-\-list | Lists the compression ratio for files that have been compressed with gzip. |
| -n<br>-\-no-name | Does not allow gzip and gunzip to preserve the original modification and access time for files. |
| -q<br>-\-quiet | Suppresses all warning messages. |
| -r<br>-\-recursive | Specifies to compress or decompress all files recursively within a specified directory. |
| -S .suffix<br>-\-suffix .suffix | Specifies a file suffix other than .gz when compressing or decompressing files. |
| -t<br>-\-test | Performs a test decompression such that a user can view any error messages before decompression, when used with the gunzip command; it does not decompress files. |
| -v<br>-\-verbose | Displays verbose output (compression ratio and filenames) during compression and decompression. |

Table 11-2 Common options used with the gzip command

As with compress and gzip, symbolic links are only compressed if the -f option is used, and the -v option can be used to display compression ratios. Also, file ownership, modification, and access time are preserved during compression.

The filename extension given to files compressed with bzip2 is .bz2. To compress the samplefile and samplefile2 files and view their compression ratios and filenames, you can use the following commands:

```
[root@server1 ~]# bzip2 -v samplefile samplefile2
samplefile: 2.637:1, 3,034 bits/byte, 62.08% saved, 20239 in, 7675 out.
```