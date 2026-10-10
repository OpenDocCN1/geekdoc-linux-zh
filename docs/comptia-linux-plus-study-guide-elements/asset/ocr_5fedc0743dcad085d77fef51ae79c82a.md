combine the `--create` (or `-o`) option with one or more of the options in Table 7.11; to restore data, you’ll do the same but use `--extract` (or `-i`). In either case, `cpio` acts on filenames that you type at the console. In practice, you’ll probably use the redirection operator (<) to pass a filename list to the program.

**TABLE 7.11** Options for use with `cpio`

| Option | Abbreviation | Description |
| :--- | :--- | :--- |
| `--reset-access-time` | `-a` | Resets the access time after reading a file so that it doesn’t appear to have been read. |
| `--append` | `-A` | Appends data to an existing archive. |
| `--pattern-file=filename` | `-E` *filename* | Uses the contents of *filename* as a list of files to be extracted in copy-in mode. |
| `--file=filename` | `-F` *filename* | Uses *filename* as the `cpio` archive file; if this parameter is omitted, `cpio` uses standard input or output. |
| `--format=format` | `-H` *format* | Uses a specified format for the archive file. Common values for *format* include `bin` (the default, an old binary format), `crc` (a newer binary format with a checksum), and `tar` (the format used by `tar`). |
| N/A | `-I` *filename* | Uses the specified *filename* instead of standard input. (Unlike `-F`, this option does not redirect output data.) |
| `--no-absolute-filenames` | N/A | In copy-in mode, extracts files relative to the current directory, even if filenames in the archive contain full directory paths. |
| N/A | `-O` *filename* | Uses the specified *filename* instead of standard output. (Unlike `-F`, this option does not redirect input data.) |
| `--list` | `-t` | Displays a table of contents for the input. |
| `--unconditional` | `-u` | Replaces all files, without first asking for verification. |
| `--verbose` | `-v` | Displays filenames as they’re added to or extracted from the archive. When used with `-t`, displays additional listing information (similar to `ls -l`). |