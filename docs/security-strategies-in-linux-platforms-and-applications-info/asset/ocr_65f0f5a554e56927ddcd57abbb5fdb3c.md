# 438 PART 3 | Building a Layered Linux Security Strategy

| TABLE 14-5 Options for the rsync command. |
| OPTION | DESCRIPTION |
| -a | Archive mode, equivalent to -rlptgoD |
| -D | Device files |
| -e | Transfer over a remote shell option such as RSH or SSH |
| -g | Group ownership |
| -H | Hard-linked files |
| -l | Soft-linked files |
| -o | User ownership |
| -p | Permissions |
| -r | Recursive mode |
| -z | Compressed data transfer |

# The rsync Command

For pure backups, the rsync command may make more sense. Unlike the dd command, it does not include the free space in a disk or partition in the backup. It copies the actual files to the remote system. In addition, the rsync command is efficient; the second time it's used to copy a filesystem, all it transmits is anything that changed. That makes the rsync command well suited to backing up data over a network.

One of the problems originally associated with the rsync command is that it transmits data in clear text, using the Remote Shell (RSH) protocol. With the help of the -e ssh switch, rsync data is encrypted and transmitted over an SSH connection in encrypted format. In fact, one version of the rsync command does more. For example, the following command backs up user home directories to the /backup/ directory on the remote system:

```
# rsync -aHz -e ssh /home/bkadmin@bkserver:/backup/
```

The command prompts for either the password or the passphrase for the bkadmin user, in archive (-a) mode, copying hard-linked (-H) files, in compressed (-z) format. Since archive mode incorporates a number of options, you may want to refer to Table 14-5 for a list of rsync command options.