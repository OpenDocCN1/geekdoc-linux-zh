# Expected Next File <number>, Got <number>

A file that was not listed in the directory showed up. This can occur when using a dump created on an active file system.

# Incremental Dump Too Low

When doing incremental restore, a dump that was written before the previous incremental dump, or that has too low an incremental level has been loaded.

# Incremental Dump Too High

When doing incremental restore, a dump that does not begin its coverage where the previous incremental dump left off, or that has too high an incremental level has been loaded.

# Tape Read Error While Restoring <filename>, Tape Read Error While Skipping Over Inode <number>, Tape Read Error While Trying To Resynchronize

A tape (or other media) read error has occurred. If a file name is specified, then its contents are probably partially wrong. If an inode is being skipped or the tape is trying to resynchronize, then no extracted files have been corrupted, though files may not be found on the tape.

# Resync Restore, Skipped <num> Blocks

After a dump read error, restore may have to resynchronize itself. This message lists the number of blocks that were skipped over.

# FILES

+   - /dev/rmt? the default tape drive
+   - /tmp/rstdir* file containing directories on the tape.
+   - /tmp/rstmode* owner, mode, and timestamps for directories.
+   - ./restoresymtable information passed between incremental restores.