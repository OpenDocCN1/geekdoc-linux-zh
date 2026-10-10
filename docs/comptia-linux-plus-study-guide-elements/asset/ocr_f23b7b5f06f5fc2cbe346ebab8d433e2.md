# **TABLE 7.8** tar Commands

| Command | Abbreviation | Description |
| :--- | :--- | :--- |
| --create | c | Creates an archive |
| --concatenate | A | Appends tar files to an archive |
| --append | r | Appends non-tar files to an archive |
| --update | u | Appends files that are newer than those in an archive |
| --diff or --compare | d | Compares an archive to files on disk |
| --list | t | Lists archive contents |
| --extract or --get | x | Extracts files from an archive |

# **TABLE 7.9** tar Qualifiers

| Command | Abbreviation | Description |
| :--- | :--- | :--- |
| --directory dir | C | Changes to directory dir before performing operations |
| --file [host:]file | f | Uses file called file on computer called host as the archive file |
| --listed-incremental file | g | Performs incremental backup or restore, using file as a list of previously archived files |
| --one-file-system | l (on older versions only) | Backs up or restores only one filesystem (partition) |
| --multi-volume | M | Creates or extracts a multitape archive |
| --tape-length N | L | Changes tapes after N kilobytes |
| --same-permissions | p | Preserves all protection information |
| --absolute-paths | P | Retains the leading / on filenames |