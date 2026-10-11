Figure 10.3 shows a similar file in a logging file system, and what happens when it is being modified.

![](bbox=[0.04, 0.15, 0.95, 0.54])

Notice how everything that is changed is appended at the end of the log.

This speeds up things, because the disk doesn't need to seek all over the disk to write to parts of a file. Also it's much safer, because the original data blocks of the file aren't “lost” until the log has successfully written the “new” data blocks. This leads to very stable file systems with nearly no fsck time required after a crash. Such file systems come back online after a crash almost immediately, because only the file system updates after the last checkpoint must be checked.

All the changes in the log can be reapplied quickly. The corrupted part of the disk is always the last change added to the log, and it can be thrown away as invalid. The only data lost will be the single change that was lost at power-off. Metadata logging file systems of 20GB and more typically take 4 or 5 seconds to fsck and repair after a crash. Thus, a metadata logging file system can make the difference between mounting a heavily populated file system in a few seconds or in 10 or more hours without a log.