and can withstand the loss of any single disk. RAID-Z is sometimes called *RAID-Z1*.

You can't add or remove disks in a RAID-Z. If you create a five-disk RAID-Z, it will remain a five-disk RAID-Z forever. Don't go thinking you can add an additional disk to a RAID-Z for more storage. You can't.

If you're using disks over 2TB, there's a nontrivial chance of a second drive failing as you repair the first drive. For large disks, you should probably consider RAID-Z2.

# ## RAID-Z2

RAID-Z2 stripes parity and data across every disk in the VDEV, much like RAID-Z1, but doubles the amount of parity information. This means a RAID-Z2 can withstand the loss of up to two disks. You can't add or remove disks from a RAID-Z2. It is slightly slower than RAID-Z.

A RAID-Z2 must have four or more disks.

# ## RAID-Z3

Triple parity is for the most important data or those sysadmins with a whole bunch of disks and no time to fancy about. You can lose up to three disks in your RAID-Z3 without losing data. As with any other RAID-Z, you can't add or remove disks from a RAID-Z3.

A RAID-Z3 must have five or more disks.

# ## Log and Cache VDEVs

Pools can improve performance with special-purpose VDEVs. Only adjust or implement these if performance problems demand them; don't add them proactively.¹ Most people don't need them, so I won't go into details, but you should know they exist in case you get unlucky.

The *Separate Intent Log* (SLOG or ZIL) is ZFS's filesystem journal. Pending writes get dumped to the SLOG and then arranged more properly in the primary pool. Every pool dedicates a chunk of disk space for a SLOG, but you can use a separate device for the SLOG instead. You need faster writes? Install a really fast drive and dedicate it to the