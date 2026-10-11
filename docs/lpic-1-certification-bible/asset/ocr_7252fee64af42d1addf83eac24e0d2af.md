Table 6-19 (continued)

| Option | Use |
| :--- | :--- |
| `-f` | Forces compression. |
| `-d` | Uncompresses the specified file. |
| `-V` | Displays version information. |
| `-v` | Verbosely displays information. |


The `compress` and `uncompress` utilities also use the standard syntax used by the `gzip` utility. The correct syntax is as follows:

```
compress -options FILENAME
```

# bzip2

Another commonly used compression utility is `bzip2`. As with the `gzip` and `compress` utilities, the permissions, ownership, and file modification times remain intact. The original file is replaced with a compressed file of the same name ending in the `.bz2` extension. These files can be uncompressed using the `bunzip2` utility. The options that can be used with the `bzip2` utility are shown in Table 6-20.

Table 6-20
Options Used with bzip2

| Option | Use |
| :--- | :--- |
| `-c` | Results are sent to standard output while the file is left intact. This ensures that the original file is preserved. |
| `-d` | Decompresses the specified file. |
| `-z` | Compresses the specified file. |
| `-t` | Perform a trial compression of the specified file. |
| `-f` | Forces files to be overwritten. |
| `-k` | Keeps the original file when compressing or decompressing. |
| `-q` | Suppresses warning messages. |
| `-V` | Displays version information. |
| `-v` | Verbosely displays information. |