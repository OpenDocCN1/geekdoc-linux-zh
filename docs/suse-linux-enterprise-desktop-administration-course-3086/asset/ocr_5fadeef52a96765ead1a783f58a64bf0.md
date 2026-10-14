# find

To search for files on the command line, you can use the `find` command. The following is the syntax for the find command:

```
find path criterion action
```

The command has a large number of options, a few of which are explained here. You can use the following arguments with the command:

+   - *path*—The section of the file system to search (the specified directory and all its subdirectories). If nothing is specified, the file system below the current directory is searched.
+   - *criterion*—The properties the file should have are shown in Table 7-19.

| Option | Description |
|---|---|
| `--ctime [+/-]days` | Searches for files whose last change took place no later than (no earlier than) a specified number of days ago. |
| `--gid number` | Searches for files with the GID (Group ID) number. |
| `--group name` | Searches for files that are owned by the group name. Instead of a name, the numeric GID is allowed. |
| `--name pattern` | Searches for files whose names contain the given pattern. If the pattern contains metacharacters (for instance `$` or wildcards, they must be enclosed in quotation marks. Otherwise, it will be interpreted by the shell and not by the find command. |
| `--size [+/-]size` | Matches files that are above or below a certain size. As an argument, the size (in blocks of 512 bytes) is given. The suffix `c` switches to byte and `k` to blocks of 1024 bytes. A preceding `+` stands for all larger files and a `-` for all smaller files. |
| `--type file_type` | Searches for a file type. A file type can be one of the following: `d` for a directory, `f` for a file, or `l` for a symbolic link. |
| `--uid number` | Searches for files with the UID (User ID) number. |
| `--user name` | Searches for files that are owned by user name. Instead of a name, the numeric UID is allowed. |

Table 7-19

+   - *action*—Options that influence the following conditions or control the search as a whole, such as the following:
+     - `print` (default)
+     - `exec command`