In this example, the `dd` command is used to copy a file from the Linux boot partition to another partition formatted using the FAT file system. This command is also useful when converting files from ASCII to EBCDIC, the Extended Binary Coded Decimal Interchange Code used by IBM, such as when working with tape backup systems.

# ## Moving files

It is possible to move a file manually by copying it to the new location and erasing the original file. However, Linux includes a command for moving files that automates these tasks. The `mv` command (short for *move*) allows you to move and rename files on Linux systems. This command works much like the `cp` command covered earlier in the chapter, using the same command syntax. The options used with the `mv` command are a bit different and are covered in Table 6-9.

Table 6-9  
Options Used with `mv`

| Option | Use |
| :----- | :--- |
| `-f`   | Removes existing files without prompting. |
| `-i`   | Prompts the user before overwriting files. |
| `-u`   | Specifies that files are not moved to a destination with the same or newer modification times. |
| `-v`   | Verbosely prints the names of files as they are moved. |

In the following example, all filenames matching the pattern beginning with `file` are moved verbosely to the `myfiles` directory.

```
```bash
# mv -v file* myfiles
fileaa -> myfiles/fileaa
fileab -> myfiles/fileab
fileac -> myfiles/fileac
filead -> myfiles/filead
fileae -> myfiles/fileae
filespace -> myfiles/filespace
```
```

In the second example, the directory `myfiles` is renamed to `files`.

```
```bash
# mv myfiles files
```
```