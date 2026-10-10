```
# tar cvlpf /dev/nst0 /directory/to/backup
# mt -f /dev/nst0 offline
```

These commands rewind the tape, space past the first file, create a new backup, and then unload the tape. Such commands are particularly useful when performing incremental backups, as described shortly.

# Performing Network Backups with rsync

Some sites implement network-enabled backup tools. Some programs, such as AMANDA, are designed for this purpose; but in many cases simpler tools will do the job, particularly for limited backups, such as backups of user data. One of these simpler tools is rsync. This program synchronizes files on one computer with those on another, enabling painless backup of specified directories. You might set up one system with a large hard disk and tape backup drive to hold backups and then have several other computers use rsync to copy critical user files onto the backup server. The syntax for the rsync client is as follows:

```
rsync [options] user-files destination
```

Table 7.15 summarizes the most important rsync options. user-files are files to be backed up, and destination is a path to the destination. user-files or destination may be either local files (indicated using a normal Linux pathname) or a remote system (indicated by a leading hostname, and optionally a username, as in fred@back.luna.edu:/archives).

**TABLE 7.15 rsync Operations**
| Operation | Operation Abbreviation | Description |
|---|---|---|
| `--archive` | `-a` | Archive mode; equivalent to -rptgoD. |
| `--recursive` | `-r` | Recurses into subdirectories. |
| `--dirs` | `-d` | Transfers directories without recursing. |
| `--links` | `-l` | Copies symbolic links as such. |
| `--copy-links` | `-L` | Copies symbolic links as referent files. |
| `--hard-links` | `-H` | Copies hard links as such. |
| `--perms` | `-p` | Preserves permissions. |
| `--executability` | `-E` | Preserves execute permissions. |
| `--owner` | `-o` | Preserves ownership. |
| `--group` | `-g` | Preserves group ownership. |