# Task 7.5: Incremental Backups

In the world of system administration, there are two types of backups that are necessary—full backups, in which every file in the file system is copied or archived, and incremental backups, in which only those files that have changed since the previous backup are saved.

A full backup is easy, and can even be accomplished by `tar -cf /dev/st0 /`, where `/dev/st0` is the name of a SCSI backup device, perhaps a DAT tape or similar.

![](bbox=[0.18, 0.47, 0.26, 0.55])

> A common backup device is a tape drive added to the SCSI chain. If that's your configuration, your tape drive is probably best referenced as `/dev/st0` for Linux, `/dev/rs0` for Darwin (though you'll have to `mknod` it before you can use it), and `/dev/rmt/0` for Solaris. There are nuances regarding whether the device will rewind or not too, so double-check with your system documentation to verify the exact device name. For example, although `/dev/st0` works for Linux, the nonrewinding device name for the same SCSI tape drive would be `/dev/nst0`.

The more interesting situation is when you want to do an incremental backup. How do you find the files that have changed since the previous backup (either a full or incremental backup, depending on what happened the previous night) and copy just those to the archival device?

You can identify files that have changed with `find`, using its super-helpful `-newer` flag, but let's focus instead on the standard Unix `dump` command, because it has this capability built in and lots more besides.

+   1. The `dump` command is built on the concept of multiple backup levels: a level 0 dump is a full backup, whereas a level 1-9 backup will only save files that have changed since the last backup of a similar, or higher level. That's confusing, I admit, so instead just use two levels like most people: 0 for full backups, 1 for incremental backups.

![](bbox=[0.18, 0.82, 0.26, 0.9])

> The `dump` command on Solaris is for programmers who want to analyze the contents of binary executables. The equivalent backup command is called `ufsdump` (and `ufsrestore`), which otherwise work completely identically to what's demonstrated here.