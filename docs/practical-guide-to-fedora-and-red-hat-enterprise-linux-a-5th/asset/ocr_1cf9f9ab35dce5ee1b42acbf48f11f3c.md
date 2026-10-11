single command-line argument; the second version uses descriptive words for the same options:

```
# tar -ztvf /dev/st0
# tar --gzip --list --verbose -file /dev/st0
```

Both commands tell tar to generate a (**v**, **verbose**) table of contents (**t**, **list**) from the tape on `/dev/st0` (f, file), using **gzip** (z, **gzip**) to decompress the files. Unlike the original UNIX tar utility, the GNU version strips the leading / from absolute pathnames. The options in Table 16-1 tell the tar program what to do. You must include exactly one of these options in a tar command.

# Table 16-1  The tar utility

| Option | Effect |
|---|---|
| `--append` (-r) | Appends files to an archive |
| `--catenate` (-A) | Adds one or more archives to the end of an existing archive |
| `--create` (-c) | Creates a new archive |
| `--delete` | Deletes files in an archive (not on tapes) |
| `--diff` (-d) | Compares files in an archive with disk files |
| `--extract` (-x) | Extracts files from an archive |
| `--help` | Displays a help list of tar options |
| `--list` (-t) | Lists the files in an archive |
| `--update` (-u) | Like the -r option, but the file is not appended if a newer version is already in the archive |

The `-c`, `-t`, and `-x` options are used most frequently. You can use many other options to change how tar operates. The `-j` option, for example, compresses or decompresses the file by filtering it through **bzip2** (page 162).

# cpio: ARCHIVES FILES

The **cpio** (copy in/out) program is similar to tar but can use archive files in a variety of formats, including the one used by tar. Normally **cpio** reads the names of the files to insert into the archive from standard input and produces the archive file as standard output. When extracting files from an archive, **cpio** reads the archive as standard input.

As with tar, some options can be given in both a short, single-letter form and a more descriptive word form. However, unlike tar, the syntax of the two forms differs when the option must be followed by additional information. In the short form, you