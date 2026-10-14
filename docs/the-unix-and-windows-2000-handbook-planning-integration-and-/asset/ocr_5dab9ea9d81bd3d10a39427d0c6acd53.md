| Table 13.7 tar Options |  |
|---|---|
| Option | Description |
| -c | Creates a new tar file |
| -x | Extracts from a tar file |
| -f filename | Specifies the file on which to perform an operation |
| -v | Specifies verbose output |
| -p | Retains file modes and ACLs |
| -t | Shows table of contents of specified tar file |

```
#tar -xvf /dev/rmt0 /home/restoredir
```

This command will extract the files from the tape and place them in the directory /home/restoredir. It should be noted that by default, tar does not restore files with the ownership and permissions on the original files unless you use the -p option:

```
#tar -xvp f /dev/rmt0 /home/restoredir
```

Table 13.7 shows a list of common tar options that can be used as part of your backup procedures.

![](bbox=[0.045, 0.82, 0.95, 0.9])

# Platform-specific Backup Utilities

There was once a time when almost every UNIX platform used the commands dump and restore to back up files from disk to a specified tape medium. As UNIX evolved and matured, each flavor of UNIX migrated to its own variant of the dump and restore commands. Table 13.8 shows some of the different commands you can use to back up your UNIX platforms. Note that for all but Linux, each program works at the filesystem level. Before you run the commands below, make sure to read the man page thoroughly for any additional commands, or to determine if it is recommended to unmount a filesystem or bring the system to single-user mode.

Table 13.9 gives examples of the same commands that need to be used when restoring data from backup media. Something that is common to all of these commands is the -i option, which allows for interactive restores. If