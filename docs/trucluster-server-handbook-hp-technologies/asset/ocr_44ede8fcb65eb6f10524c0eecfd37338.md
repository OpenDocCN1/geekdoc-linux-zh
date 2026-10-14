```
# cnxread -q dak2
The CNX Partition info for /dev/rdisk/dsk2h. This is a member boot disk.
Quorum Section Information:

nada (CSID: 0, incarn: 0)

# Members - Current Votes - Quorum Votes - Qdisk Votes
0           0           0           0

Qdisk claimed on 19691232 at 19:00:00 by member:
nobody (CSID: 0, incarn: 0, memberid: 0)

Qdisk written on 19691232 at 19:00:00 by member:
nobody (CSID: 0, incarn: 0, memberid: 0)
Activity count = 0
```

The quorum section contains nothing of interest on a member disk.

# 17.8.5.1.2 Partition in Time (PIT) Segment

As of this writing, the PIT segment has been reserved for future use.

# 17.8.5.1.3 AdvFS cluster_root Devices Segment

This segment is defined in the clupt.h file as containing the following information:

+   - A magic number
+   - A data sequence number
+   - The number of devices in the cluster_root domain
+   - An array of device IDs

Using the cnxread program to look at a member's boot disk cnx partition, we can see that the cluster_root domain has only one device.

```
# cnxread dsk2
The CNX Partition info for /dev/rdisk/dsk2h. This is a member boot disk.
Cluster Root Filesystem (AdvFS) Segment Information

Magic #: 0x42534, Sequence #: 88

      maj,min
      ----
Devices: { 1}: 19, 52
```