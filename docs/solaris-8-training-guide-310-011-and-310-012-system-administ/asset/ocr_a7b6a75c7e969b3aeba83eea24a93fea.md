# TABLE 11.13 continued

# COMMAND OPTIONS FOR ufsrestore

| Option | Description |
|---|---|
| t <filename(s)> | Table of contents. Checks the files specified in the <filename(s)> argument against the medium. For each file, the full filename and the inode number (if the file is found) are listed. If the filename is not found, ufsrestore indicates that the file is not on the “volume,” meaning any volume in a multi-volume dump. If you do not enter the <filename(s)> argument, all files on all volumes of the medium are listed without distinguishing on which volume the files are located. When you use the h option, only the directory files specified in <filename(s)>—not their contents—are checked and listed. The table of contents is read from the first volume of the medium or (if you use the a option) from the specified archive file. This option is mutually exclusive with the x and r options. |
| b <factor> | Blocking factor. Specifies the number of 512-byte blocks to read from tape per operation. By default, ufsrestore tries to figure out the block size used in writing the tape. |
| m | Restores specified files into the current directory on the disk, regardless of where they are located in the backup hierarchy, and renames them with their inode number. For example, if the current working directory is /files, a file in the backup named ./database/test with inode number 156 is restored as /files/156. This option is useful when you are extracting only a few files. |
| s<n> | Skips to the nth backup file on the medium. This option is useful when you put more than one backup on a single tape. |
| v | Verbose. Displays the name and inode number of each file as it is restored. |

For a full listing, refer to the Solaris online manual pages.

Table 11.14 lists the commands that can be used with ufsrestore when using interactive mode (ufsrestore -i).