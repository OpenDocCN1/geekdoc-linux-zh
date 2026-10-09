Bstdar, like any other tar(1), can be dumb. If your filesystem is corrupt in any way, bstdar will back up what it thinks you asked for. It will then happily restore files that were damaged during the original backup, overwriting working-but-incorrect files with not-working-and-still-incorrect versions. These sorts of problems rarely happen, but tend to be unforgettable when they do.

# FILESYSTEM COHERENCE

No matter what backup software you use, files can change as you’re trying to back them up. Log files constantly add stuff at the end, while databases can change anywhere in the file. Filesystem snapshots are always consistent, and both UFS (Chapter 11) and ZFS (Chapter 12) support them. Never back up live databases; instead, dump the database to an archive file and back up that archive.

# tar Modes

Tar can perform several different actions, controlled by the command line flags. These different actions are called *modes*. You’ll need to read the man page for a complete description of all tar modes, but the following list describes the most commonly used ones.

# Create an Archive

Use *create mode* (-c) to create a new archive. Unless you specify otherwise, this flag backs up everything to your tape drive ($TAPE, or /dev/sa0 if you haven’t set $TAPE). To back up your entire system, you’d tell tar to archive everything from the root directory down:

```
`# tar -c /`
```