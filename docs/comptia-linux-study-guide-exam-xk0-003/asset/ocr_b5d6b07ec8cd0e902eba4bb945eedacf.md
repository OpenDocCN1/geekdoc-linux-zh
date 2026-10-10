**TABLE 7.9** **tar Qualifiers** *(continued)*

| Command | Abbreviation | Description |
| :--- | :--- | :--- |
| `--verbose` | v | Lists all files read or extracted; when used with `--list`, displays file sizes, ownership, and time stamps |
| `--verify` | W | Verifies the archive after writing it |
| `--exclude` *file* | (none) | Excludes *file* from the archive |
| `--exclude-from` *file* | X | Excludes files listed in *file* from the archive |
| `--gzip` or `--ungzip` | z | Processes archive through `gzip` |
| `--bzip2` | j (some older versions used I or y) | Processes archive through `bzip2` |

Of the commands listed in Table 7.8, the most commonly used are `--create`, `--extract`, and `--list`. The most useful qualifiers from Table 7.9 are `--file`, `--listed-incremental`, `--one-file-system`, `--same-permissions`, `--gzip`, `--bzip2`, and `--verbose`. If you fail to specify a filename with the `--file` qualifier, tar will attempt to use a default device, which is often (but not always) a tape device file.

A typical tar command to extract files from a tarball looks like this:

```
```shell
# tar --extract --verbose --gunzip --file samba-3.2.11.tar.gz
```
```

This command can be expressed somewhat more succinctly using command abbreviations:

```
```shell
# tar xvvf samba-3.2.11.tar.gz
```
```

In either form, this tar command extracts files from `samba-3.2.11.tar.gz` to the current directory. Most tarballs include entire directory trees, so this command results in one or more directories being created, if they don't already exist, as well as files within the directories.

![](bbox=[0.15, 0.87, 0.21, 0.93])

> Before extracting a tarball, use the `--list` command to find out what files and directories it contains. This information can help you locate the files stored in the tarball. In addition, it can help you spot problems before they would occur in case a tarball does *not* contain a neat directory structure but instead contains files that would all be dropped in the current directory.