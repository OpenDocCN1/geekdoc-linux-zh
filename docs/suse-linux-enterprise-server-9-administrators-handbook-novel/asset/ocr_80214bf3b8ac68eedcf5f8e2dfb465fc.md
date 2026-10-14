+   - **Copy-pass mode—** `cpio -p` reads from stdin a list of filenames and copies these files from one directory tree to another, essentially combining the copy-out and copy-in steps without actually using an archive.

Similar to `tar`, `cpio` uses many command-line switches. Table 10.6 shows a list of the most commonly used options.

**TABLE 10.6**  
**Commonly Used Options for cpio**

| OPTION | DESCRIPTION |
|---|---|
| `-A` | Appends to the existing archive. The archive must be specified using either `-F` or `-O`, valid only in copy-out mode. |
| `-B` | Sets the I/O block size to 5,120 bytes instead of the default 512 bytes. `-B` is meaningful only with data directed to or from a character block device such as `/dev/st0`; thus, it is meaningless in the copy-pass mode. It cannot be used in conjunction with `-C`. |
| `-C bufsize` | Sets I/O block size to `bufsize` instead of the default 512 bytes. Like `-B`, `-C` is meaningful only when using devices such as `/dev/st0`. It cannot be used in conjunction with `-B`. |
| `-f` | Copies only files that do not match any of the given patterns. |
| `-F file` | Uses `file` for the archive instead of stdin or stdout. |
| `-i` | (Copy-in mode) Extracts files from stdin. |
| `-I file` | Reads the archive from the specified file instead of stdio. This option is valid only in the copy-in mode. |
| `-o` | (Copy-out mode) Reads filenames from stdin and copies those files to stdout. This option is used mainly to copy directory trees. |
| `-O file` | Directs output to `file` instead of stdout. This option is valid only in the copy-out mode. |
| `-p` | (Copy-pass mode) Reads filenames from stdin and copies those files to stdout. This option is used mainly to copy directory trees. |
| `-t` | Prints a table of contents of the input. No files are created (mutually exclusive with `-V`). |
| `-u` | Unconditionally replaces all files, without asking whether to replace existing newer files with older ones. |
| `-v` | Turns on verbose mode. Lists the files processed. When this option is used with the `-t` option, the table of contents looks like the output from the `ls -l` command. |
| `-V` | Turns on special verbose mode. Prints a dot for each file processed. This option is useful to assure the user that cpio is working without printing out all the filenames. |