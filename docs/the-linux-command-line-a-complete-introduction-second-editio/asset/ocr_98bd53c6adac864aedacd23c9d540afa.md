the `[ command` requiring that the `]` character be provided as its final argument.

The `test` and `[` commands support a wide range of useful expressions and tests.

# File Expressions

Table 27-1 lists the expressions used to evaluate the status of files.

**Table 27-1:** test File Expressions

| Expression | Is true if: |
|---|---|
| `file1 -ef file2` | `file1` and `file2` have the same inode numbers (the two filenames refer to the same file by hard linking). |
| `file1 -nt file2` | `file1` is newer than `file2`. |
| `file1 -ot file2` | `file1` is older than `file2`. |
| `-b file` | `file` exists and is a block-special (device) file. |
| `-c file` | `file` exists and is a character-special (device) file. |
| `-d file` | `file` exists and is a directory. |
| `-e file` | `file` exists. |
| `-f file` | `file` exists and is a regular file. |
| `-g file` | `file` exists and is set-group-ID. |
| `-G file` | `file` exists and is owned by the effective group ID. |
| `-k file` | `file` exists and has its “sticky bit” set. |
| `-L file` | `file` exists and is a symbolic link. |
| `-O file` | `file` exists and is owned by the effective user ID. |
| `-p file` | `file` exists and is a named pipe. |
| `-r file` | `file` exists and is readable (has readable permission for the effective user). |