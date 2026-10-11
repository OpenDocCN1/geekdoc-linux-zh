| Partition Type | Value | Partition Type | Value |
| :--- | :--- | :--- | :--- |
| Micropart | 52 | DOS R/O | e3 |
| GNU HURD | 63 | DOS secondary | f2 |
| Novell Network 286 | 64 | BBT | ff |

Now you might be wondering how all this additional complexity is normally used. See Figure B–6, *Disk Drive With Single Partition* for an example.

# **Figure B–6** Disk Drive With Single Partition

![](bbox=[0.08, 0.38, 0.55, 0.63])

That’s right -- in many cases there is but a single partition spanning the entire disk, essentially duplicating the pre-partitioned days of yore. The partition table has only one entry used, and it points to the start of the partition.

We’ve labeled this partition as being of type "DOS," although as you can see from Table B–1, *Partition Types*, that’s a bit simplistic, but adequate for the purposes of this discussion. This is a typical partition layout for most newly purchased computers with some version of Windows pre-installed.