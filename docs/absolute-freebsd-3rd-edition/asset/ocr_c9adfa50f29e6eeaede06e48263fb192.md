As filesystems grow, soft updates show their limits. Multiterabyte filesystems still need quite a while to recover from an unplanned shutdown. The original soft updates journaling paper (http://www.mckusick.com/softdep.pdf) mentions that a 92 percent full 14-drive array with a deliberately damaged filesystem needed 10 hours for integrity checking. You’ll need a journal well before then.

# ## Soft Updates Journaling

A journaling filesystem records any changes outside the actual filesystem. Changes get quickly dumped to storage and then inserted into the filesystem at a more leisurely pace. If the system dies unexpectedly, the filesystem automatically recovers any changes from the journal. This vastly reduces the requirement for rebuilding filesystem integrity at startup. When you install FreeBSD, it defaults to creating UFS partitions with soft update journaling.

Rather than recording all transactions, the soft updates journal records all metadata updates so that the filesystem can always be restored to an internally consistent state. Benchmarks show that journaling adds only a tiny amount of load to soft updates. It does add I/O overhead, however, as the system must dump all changes to the journal and then replay them into the filesystem. It vastly reduces recovery time, however. That 14-drive array that needed 10 hours for integrity checking? It needed less than one minute to recover from the same damage using the journal.

Soft updates with journaling is very powerful. Why wouldn’t you always use journaling? Soft updates journaling disables UFS snapshots. If you need UFS snapshots, you can’t journal. If you need snapshots, though, you’re probably better off using ZFS anyway. FreeBSD’s version of dump(8) uses UFS snapshots to back up live filesystems. Only us old Unix hands use dump any more, and that’s mostly because we already know it, but if your organization mandates using dump(8), you need another resiliency option.

# ## GEOM Journaling