**TABLE 10.9**  
**Noteworthy restore Command-Line Options**

| OPTION | DESCRIPTION |
|---|---|
| `-C` | Compares the contents of the archive with the current filesystem and no restore takes place. You can use this option to check what has changed since your last backup. |
| `-f file` | Specifies the archive file. Like dump, it also defaults to `/dev/tape` and will check the TAPE environment variable if that fails. |
| `-h directory` | Extracts only the directory when specified, rather than its contents. |
| `-i` | Performs interactive restoration of specified files. This option also allows you to browse the dump image and flag files or directories to be extracted later. |
| `-r` | Allows you to rebuild the filesystem from the dump image. Use this option if you need to do bare-metal recovery from a tape. It expects a clean filesystem (that is, it expects you to have just run `mke2fs`). This operation is not interactive and should not be done unless you intend to actually restore the filesystem itself rather than just extract a couple of files. |
| `-R` | Resumes interrupted full restoration. |
| `-s fileno` | Specifies the position of the archive on the tape. This capability is useful when there are multiple dump images on the same media. |
| `-t file` | Lists filenames on the backup archive but does not restore them. |
| `-T` | Specifies the temporary directory. |
| `-v` | Produces verbose output. |
| `-x file`<br>`-X fileset` | Extracts only the named files from the archive. The uppercase `-X` instead reads a list of files to restore from a flat ASCII text file. |
| `-y` | Does not query on error. |

The restore utility is not too difficult to use but can be rather tricky when you’re dealing with multiple dump images on the same media. Therefore, you should be familiar with it before you really have to use it. The following are two sample restore commands:

+   - Retrieves all the files from the archive in tape media and writes them under the current directory:
+     ```
+     restore -rf /dev/st0
+     ```
+   - Performs an interactive restoration from the third dump image on the tape media:
+     ```
+     restore -is 3 -f /dev/st0
+     ```