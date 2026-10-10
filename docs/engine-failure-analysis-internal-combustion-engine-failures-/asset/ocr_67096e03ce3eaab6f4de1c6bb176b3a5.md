# gzexe

```
gzexe [ filename ]
```

Compresses the executable file specified by *filename* so that it automatically decompresses and executes when you run it. Although compressing an executable in this way saves disk storage space, the executable takes longer to start. The program automatically backs up the original file with the `~` suffix. You can remove this backup file when you are sure that the compressed executable runs correctly.

# OPTION

| Use This Option | To Do This |
|---|---|
| `-d` | Decompress the executable file |

# EXAMPLE

| This Command | Does the Following |
|---|---|
| `gzexe /usr/local/Office51/bin/soffice` | Compresses the specified executable so that it occupies less disk space. |

# gzip

```
gzip [ option ] *filename*
```

Compresses the specified *filename* using a patent-free compression algorithm (LZ77). For *filename*, specify the name of the file or files to be archived. You can use a shell pattern (see the section “Shell Patterns” in Chapter 4), a space-separated list of files, or a directory name. With the `-r` option, you can quickly compress all the files in a directory tree. By default, gzip does not overwrite existing output files (use the `--force` option to override this setting), but the program replaces input files with compressed files that have the `.gz` extension. To decompress the files, use gunzip.

See also compress, bzip2.