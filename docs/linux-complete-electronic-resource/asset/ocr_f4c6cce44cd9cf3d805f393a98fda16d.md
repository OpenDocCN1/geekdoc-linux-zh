+   u	Update the file /etc/dumpdates after a successful dump. The format of /etc/dumpdates is readable by people, consisting of one free format record per line: filesystem name, increment level and ctime(3) format dump date. There may be only one entry per filesystem at each level. The file /etc/dumpdates may be edited to change any of the fields, if necessary.

+   T date	Use the specified date as the starting time for the dump instead of the time determined from looking in /etc/dumpdates. The format of date is the same as that of ctime(3). This option is useful for automated dump scripts that wish to dump over a specific period of time. The T option is mutually exclusive from the u option.

+   W	dump tells the operator what file systems need to be dumped. This information is gleaned from the files /etc/dumpdates and /etc/fstab. The W option causes dump to print out, for each file system in /etc/dumpdates the most recent dump date and level, and highlights those file systems that should be dumped. If the W option is set, all other options are ignored, and dump exits immediately.

+   w	Is like W, but prints only those filesystems which need to be dumped.

dump requires operator intervention on these conditions: end of tape, end of dump, tape write error, tape open error or disk read error (if there are more than a threshold of 32). In addition to alerting all operators implied by the n key, dump interacts with the operator on dump's control terminal at times when dump can no longer proceed, or if something is grossly wrong. All questions dump poses must be answered by typing "yes" or "no," appropriately.

Since making a dump involves a lot of time and effort for full dumps, dump checkpoints itself at the start of each tape volume. If writing that volume fails for some reason, dump will, with operator permission, restart itself from the checkpoint after the old tape has been rewound and removed, and a new tape has been mounted.

dump tells the operator what is going on at periodic intervals, including usually low estimates of the number of blocks to write, the number of tapes it will take, the time to completion, and the time to the tape change. The output is verbose, so that others know that the terminal controlling dump is busy, and will be for some time.