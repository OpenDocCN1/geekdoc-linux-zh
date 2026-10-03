# TABLE 11.6

# Four Modes of Operation for pax

| Option | Operation Mode | Description |
|---|---|---|
| -r | Read mode | When -r is specified but -w is not. pax extracts the filenames and directories found in the archive file. The archive file is read from disk or tape. If an extracted file is a directory, the file hierarchy is extracted as well. The extracted files are created relative to the current file hierarchy. |
| None | List mode | When neither -r nor -w is specified. pax displays the filenames or directories found in the archive file. The archive file is read from disk, tape, or the standard input. The list is written to the standard output. |
| -w | Write mode | When -w is specified, but -r is not. pax writes the contents of the file to the standard output in an archive format specified by the -x option. If no files are specified, a list of files to copy (one per line) is read from the standard input. A directory includes all the files in the file hierarchy rooted at the file. |
| -rw | Copy mode | When both -r and -w are specified. pax copies the specified files to the destination directory. |

In addition to selecting a mode of operation, you can select one or more options from Table 11.7.

# TABLE 11.7

# COMMAND OPTIONS FOR pax

| Option | Description |
|---|---|
| -r | Reads an archive file from standard input and extracts the specified files. If any intermediate directories are needed to extract an archive member, these directories are created. |
| -w | Writes files to the standard output in the specified archive format. When no file operands are specified, standard input is read for a list of pathnames—one per line, without leading or trailing blanks. |