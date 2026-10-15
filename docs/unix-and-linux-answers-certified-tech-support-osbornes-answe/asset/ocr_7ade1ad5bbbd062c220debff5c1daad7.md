# When should I consider making tape or floppy backups?

Hard disk backups are nice, and they provide adequate protection for many purposes, especially considering that your system administrator is undoubtedly doing periodic complete tape backups. But there are circumstances where hard disk backups just aren’t appropriate. If you are doing extremely sensitive work and can’t leave copies of what you do on the hard disk, for example, you’ll need to take the work off the hard disk when you aren’t present. And if you would be totally devastated if you lost certain files, you probably want to do your own backups above and beyond what the system administrator is doing, especially if you are in an environment where the system-wide backups are done only weekly, for example.

# What’s the easiest way to make a tape or floppy backup?

The most common mechanism for backing up files to an external storage medium such as tape or floppy is the UNIX tar (tape archive and restore) command. This command, which is available on virtually all UNIX systems and can be obtained for other systems such as DOS, is a simple and fairly efficient way to handle most of a user’s backup chores. The system administrator may well have more powerful tools, which can easily span multiple machines and filesystems on the network, but fortunately you aren’t likely to need those.

The syntax for the tar command is

```
tar key files
```

where key is one of the following basic actions:

+   - c Creates a new archive
+   - r Appends to an existing archive
+   - t Lists the contents of the archive
+   - u Updates the archive, adding files that aren’t present or are newer
+   - x Extracts the files from the archive