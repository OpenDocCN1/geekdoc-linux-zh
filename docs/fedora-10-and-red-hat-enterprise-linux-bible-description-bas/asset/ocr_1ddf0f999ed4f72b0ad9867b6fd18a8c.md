# Table 13-9: Options to pax

| Options | Description |
| - | - |
| -r | Read files from an archive. |
| -w | Write files to an archive. |
| -a | Append files to a previously created archive. |
| -b blocksize | Specify the archive's data block size. It must be a multiple of 512. |
| -c pattern | Match all files except those that matched the pattern. |
| -d | Match filename wildcards against file or directory names, not the complete path. |
| -f archive | Specify the name of the archive. |
| -i | Interactively rename files when archiving. |
| -k | Do not overwrite existing files. |
| -l | Link files with hard links in copy mode (-r -w). |
| -n pattern | Match only the first file that matches the supplied pattern. |
| -o options | Extra options to specify the archiving format. |
| -p string | Specify the file characteristics to retain when archiving or copying. Read the pax man page for more information on this option. |
| -s replstr | Modify the archived filenames using the supplied regular expression. |
| -t | Preserve the access time of archived files. |
| -u | Do not overwrite files with older versions. |
| -v | Provide verbose output when running. |
| -x format | Specify the format of the archive. Valid formats include cpio, bcpio, sv4cpio, sv4c, and tar. The default is ustar when creating an archive. The pax command will automatically determine the file type when reading an archive. |
| -z | Indicates that gzip will be used to compress and decompress the archive. |
| -B bytes | Specify the number of bytes per archive volume. Use this option to create multivolume archives on removable media. |
| -D | Do not overwrite existing files with files that have an older modification time. |
| -E limit | Limit the number of files pax will retry on encountering a read or write error. |
| -G group | Select files based on a group name or GID. To select by GID, place a # sign in front of the group number. |