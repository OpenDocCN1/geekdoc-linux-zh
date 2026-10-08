# rm, rdir

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwcmdc |

# See Also

+   - rsh(1), stty(1), tty(1), in.named(1M), hosts(4), hosts.equiv(4),
ipnodes(4), noglogin(4), attributes(5)

# Diagnostics

NO LOGINS: System going down in N minutes

The system is in the process of being shut down and logins have been disabled.

# rm, rdir — Remove Directory Entries

# Synopsis

```
/usr/bin/rm [-f] [-i] file...
/usr/bin/rm -R [-f] [-i] dirname...[file...]
/usr/xpg4/bin [-fiR] file...
/usr/bin/rmdir [-ps] dirname...
```

# Description

/usr/bin/rm, /usr/xpg4/bin/rm remove files. The rm command removes the entry specified by each file argument. If a file has no write permission and the standard input is a terminal, the full set of permissions (octal) for the file is printed, followed by a question mark. The question mark is a prompt for confirmation. If your answer begins with y (yes), the file is deleted; otherwise, the file remains.

If it is a symbolic link, the link is removed but the file or directory to which it refers is not. You do not need write permission to remove a symbolic link provided you write permissions in the directory.

If you specify multiple files and removal of any files for any reason, rm writes a diagnostic message to standard error, nothing more to the current file, and goes on any remaining files.

If the standard input is not a terminal, the command operates as if you specified - option.

> Note — A enables you to explicitly mark the end of any command-line options, allowing rm to recognize file arguments that begin with a -. As an aid to BSD migration, rm accepts - as a synonym for --. This migration may disappear in a future release. If you use -- twice in the same command line, the second is interpreted as a file.