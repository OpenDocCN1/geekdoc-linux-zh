# TABLE 4.2   tar Qualifiers (*continued*)

| Qualifier | Abbreviation | Description |
| :--- | :--- | :--- |
| `--same-permissions` | `p` | Preserves all protection information |
| `--absolute-paths` | `P` | Retains the leading / on filenames |
| `--verbose` | `v` | Lists all files read or extracted; when used with `--list`, displays file sizes, ownership, and time stamps |
| `--verify` | `W` | Verifies the archive after writing it |
| `--exclude file` | (none) | Excludes *file* from the archive |
| `--exclude-from file` | `X` | Excludes files listed in *file* from the archive |
| `--gzip` or `--ungzip` | `z` | Processes an archive through `gzip` |
| `--bzip2` | `j` (some older versions used `I` or `y`) | Processes an archive through `bzip2` |

Of the commands listed in Table 4.1, the most commonly used are `--create`, `--extract`, and `--list`. The most useful qualifiers from Table 4.2 are `--file`, `--listed-incremental`, `--one-file-system`, `--same-permissions`, `-zgzip`, `-zbzip2`, and `--verbose`. If you fail to specify a filename with the `--file` qualifier, tar will attempt to use a default device, which is often (but not always) a tape device file.

As an example, consider archiving and compressing the *my-work* subdirectory of your home directory to a USB pen drive mounted at */media/pen*. The following command will do the trick:

```
`$ tar cvfz /media/pen/my-work.tgz ~/my-work`
```

If you then transfer this pen drive to another system, mount it at */media/usb*, and want to extract the archive, you can do so with another command:

```
`$ tar xvzf /media/usb/my-work.tgz`
```

This command creates a subdirectory called *my-work* in the current working directory and populates it with the files from the archive. If you don't know what's in an archive, it's a good practice to examine it with the `--list` command before extracting its contents. Although common practice has tarballs with a single subdirectory, sometimes tarballs drop many files in the current working directory, which can make them difficult to track down if you run the command in a directory that already has many files.