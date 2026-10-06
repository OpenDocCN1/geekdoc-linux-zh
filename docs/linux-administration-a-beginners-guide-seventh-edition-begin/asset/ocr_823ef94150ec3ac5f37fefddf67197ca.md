```
[root@server ~] # dump -outf /dev/sda6 | gzip --fast -c >> /dev/nst0
[root@server ~] # mt -f /dev/nst0 rewind
[root@server ~] # mt -f /dev/nst0 eject
```

The first mt command makes the tape is completely rewound and ready to accept data. Then come all dump commands run on the partitions, with their outputs piped through gzip before going to the tape. To make the backups go a little faster, the --fast option is used with gzip. This results in compression that isn't as good as normal gzip compression, but it's much faster and takes less CPU time. The -c option on gzip tells it to send its output to the standard out. We then rewind the tape and eject it.

# Using restore

The restore program reads the dump created by dump and extracts individual files and directories from them. Although restore is a command-line tool, it offers a more intuitive mode that lets you go through a directory structure from the tape. Table 31-3 shows the command-line options for the restore utility.

| Option | Description |
|---|---|
| -i | Enables interactive mode for restore. The utility will read the directory contents of the tape and give you a shell-like interface in which you can move directories around and tag files you want to recover. When you've tagged all the files you want, restore will go through the dump and restore those files. This mode is handy for recovering individual files, especially if you aren't sure which directories they're |
| -r | Rebuilds a file system. If you lose everything in a file system (via a disk failure, for instance), you can simply re-create an empty file system and restore all the files and directories of the dump |
| -b blocksize | Sets the dump's block size to kilobytes. If you don't supply this information, restore will figure this out for you |
| -f filename | Reads the dump from file filename |
| -T directory | Specifies the temporary workspace (directory) for restore. The default is /tmp |
| -v | The verbose option; it shows each step restore is taking |
| -Y | In the event of an error, automatically retries instead of asking the user if she wants to retry.|

# Table 31-3 Command-Line Options for the restore Utility