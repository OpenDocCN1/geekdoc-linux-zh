```
should start with the last volume and work toward the first.
specify next volume #: 1
set owner/mode for '.*' [lyn] y
restore >
```

At this point, the files have been recovered, and you can exit the `restore` program by issuing the `quit` command. That's all there is to it. You now know the basics of using the `dump` and `restore` commands.

# Configuring Amanda for Network Backups

Using Amanda (the Advanced Maryland Automatic Network Disk Archiver), you can use a single large-capacity tape drive on a server to back up files from multiple computers over a network. The Amanda packages (`amanda`, `amanda-client`, and `amanda-server`) include a variety of commands. The online man page for Amanda describes the commands as shown in Table 12-7.

**TABLE 12-7**

**Backup Commands Used with Amanda**

| Command | Description |
| :--- | :--- |
| **amdump** | Do automatic Amanda backups. This command is normally run by `cron` on a computer called the **tape server host** and requests backups of file systems located on backup clients. `amdump` backs up all disks in the `disklist` file to tape or, if there is a problem, to a special holding disk. After all backups are done, `amdump` sends mail reporting failures and successes. |
| **amflush** | Flush backups from the holding disk to tape. `amflush` is used after `amdump` has reported it could not write backups to tape. When this happens, backups stay in the holding disk. After the tape problem is corrected, run `amflush` to write backups from the holding disk to the tape. |
| **amcleanup** | Clean up after an interrupted `amdump`. This command is needed only if `amdump` was unable to complete for some reason, usually because the tape server host crashed while `amdump` was running. |
| **amrecover** | Provide an interactive interface to browse the Amanda index files and select which tapes to recover files from. `amrecover` can also run `amrestore` and the system restore program (such as `tar`) sometimes. |
| **amrestore** | Read an Amanda tape, searching for requested backups. `amrestore` is suitable for everything from interactive restores of single files to a full restore of all partitions on a failed disk. |

continued