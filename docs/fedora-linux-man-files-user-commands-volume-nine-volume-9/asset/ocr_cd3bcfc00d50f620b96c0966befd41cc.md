into the file specified by the **--log-file** option (which st also be specified for this option to have any effect). If you specify an empty string, updated files will not be ntioned in the log file. For a list of the possible escape characters, see the “log format” setting in the rsyncd.conf mnpage. The default FORMAT used if **--log-file** is specified and this option is not is '%i %n%n%L'. **--stats** This tells rsync to print a verbose set of statistics on the file transfer, allowing you to tell how effective rsync's delta-transfer algorithm is for your data. This option is equivalent to **--info=stats2** if coined with 0 or 1 **-v** options, or **--info=stats3** if coined with 2 or more **-v** options. The current statistics are as follows:

+   o

+   *   **Nuer of files** is the count of all "files" (in the generic sense), which includes directories, syinks, etc. The total count will be followed by a list of counts by filetype (if the total is non-zero). For example: "(reg: 5, dir: 3, link: 2, dev: 1, special: 1)" lists the totals for regular files, directories, syinks, devices, and special files. If any of value is 0, it is completely omitted from the list.

+   o

+   *   **Nuer of created files** is the count of how many "files" (generic sense) were created (as opposed to updated). The total count will be followed by a list of counts by filetype (if the total is non-zero).

+   o

+   *   **Nuer of deleted files** is the count of how many "files" (generic sense) were created (as opposed to updated). The total count will be followed by a list of counts by filetype (if the total is non-zero). Note that this line is only output if deletions are in effect, and only if protocod 31 is being used (the default for rsync 3.1.x).

+   o

+   *   **Nuer of regular files transferred** is the count of normal files that were updated via rsync's delta-transfer algorithm, which does not include dirs, syinks, etc. Note that rsync 3.1.0 added the word “regular” into this heading.

+   o

+   *   **Total file size** is the total sum of all file sizes in the transfer. This does not count any size for directories or special files, but does include the size of syinks.

+   o

+   *   **Total transferred file size** is the total sum of all files sizes for just the transferred files.

+   o

+   *   **Literal data** is how ch unmatched file-update data we had to send to the receiver for it to recreate the updated files.

+   o

+   *   **Matched data** is how ch data the receiver got locally when recreating the updated files.

+   o

+   *   **File list size** is how big the file-list data was when the sender sent it to the receiver. This is smaller than the in-mory size for the file list due to so compressing of duplicated data when rsync sends the list.

+   o