| Pax Command | Description |
| :--- | :--- |
| pax -r -w /olddir /newdir | Copy the entire contents of the directory /olddir into a new directory called /newdir. |
| pax -w -B 1440000 -f /dev/fd0 * | Archive the contents of the current directory onto multiple floppy disks. |
| pax -w -x cpio -f myfiles * | Archive the contents of the current directory into an archive file named myfiles using the cpio format. |
| pax -r -U mary -f backups | Extract all of the files owned by user mary from the archive named backups. |

Note that by leaving off both the -r and -w options, you cause pax to simply list the contents of the archive. If you specify both the -r and -w options, then you should leave off the -f option and supply source and destination directories instead. This will cause the source directory to be completely cloned in the specified destination directory.

You can use additional parameters to further modify pax's behavior. For example, you may use the -x option in conjunction with the -w option to specify the specific archive type to create, or you may use the -B option to specify the number of bytes to write to each volume of a multi-volume archive.

Table 13-9 briefly describes the many optional parameters to the pax command.

# Table 13-9: Options to pax

| Pax Options | Description |
| :--- | :--- |
| -r | Read files from an archive. |
| -w | Write files to an archive. |
| -a | Append files to a previously created archive. |
| -b blocksize | Specify the archive's data block size. It must be a multiple of 512. |
| -c | Match all files except those that match the specified pattern. |
| -d | Match filename wildcards against file or directory names only, not the complete path. |
| -f archive | Specify the name of the archive. |
| -i | Interactively rename files when archiving. |
| -k | Do not overwrite existing files. |
| -l | Link files with hard links when in copy mode (-r -w). |
| -n | Match only the first file that matches the supplied pattern. |
| -o options | Extra options specific to the archiving format used. |