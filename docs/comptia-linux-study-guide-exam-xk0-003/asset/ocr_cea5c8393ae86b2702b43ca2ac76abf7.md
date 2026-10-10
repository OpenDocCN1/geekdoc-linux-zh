**TABLE 7.15**   *rsync Operations (continued)*

| Operation | Operation Abbreviation | Description |
|---|---|---|
| `--times` | `-t` | Preserves time stamps. |
| `--devices` | none | Preserves device files. |
| `--special` | none | Preserves special files. |
| none | `-D` | Same as `--devices --special`. |
| `--dry-run` | `-n` | Shows what would happen without actually transferring files. |
| `--one-file-system` | `-X` | Copies from a single filesystem, not from mounted filesystems. |
| `--compress` | `-z` | Compresses files during transfer. This has no effect on file size on the server. |
| `--progress` | none | Shows progress indicator during transfer. |

Other protocols may be used for network backups, of course. The File Transfer Protocol (FTP), the Secure Shell (SSH), Network FileSystem (NFS), and others can all handle basic data transfer tasks. The main advantage of `rsync` is that it transfers only the data that must be transferred to keep the remote archive up-to-date. This fact helps minimize network bandwidth use, which can be an important factor when backing up many or large systems over your network.

# # Planning a Backup Schedule

Regular computer backup is important, but precisely *how* regularly is a matter that varies from one system to another. If a computer’s contents almost never change (as might be true of a dedicated router or a workstation whose user files reside on a file server), backups once a month or even less often might be in order. For critical file servers, once a day is not too often. You’ll have to decide for yourself just how frequently your systems require backup. Consider factors such as how often the data change, the importance of the data, the cost of recovering the data without a current backup, and the cost of making a backup. Costs may be measured in money, your own time, users’ lost productivity, and perhaps lost sales.

Even the most zealous backup advocate must admit that creating a full backup of a big system on a regular basis can be a tedious chore. A backup can easily take several hours, depending on backup size and hardware speed. For this reason, most backup packages, including *tar*, support *incremental backups*. You can create these using the `-l-listed-incremental` *file* qualifier to *tar*. Subsequent backups back up only new or changed files.