# Drawbacks of RAID 5

for administering RAID hardware already integrated, however: see Disk Array
under Devices in SMIT.

# Disk failure recovery

The Google disk failure study cited on page 211 should be pretty convincing evi-
of the need for some form of storage redundancy in most production envi-
ronments. At an 8% annual failure rate, your organization needs only 150 hard
disks in service to expect an average of one failure per month.

JBOD and RAID 0 modes are of no help when hardware problems occur; you\must recover your data manually from backups. Other forms of RAID enter a
degrad mode when the offending devices are marked as faulty. The RAID
arrays continue to function normally from the perspective of storage clients, al-
ough perhaps at reduced performance.

Bad disks must be swept out for new ones as soon as possible to restore red-
dancy to the array. A RAID 5 array or two-disk RAID 1 can only tolerate the
failure of a single device. Once that failure has occurred, the array is vulnerable to
a second failure.

The specifics of the process are usually pretty simple. You replaced the failed disk
with another of similar or greater size, then tell the RAID implementation to re-\place the old disk with the new one. What follows is an extended period during
which the parity or mirror information is rewritten to the new, black disk. This
is an overnight operation. The array remains available to clients during this
phase, but performance is likely to be very poor.

To limit downtime and the vulnerability of the array to a second failure, most
RAID implementations let you designate one or more disks as "hot" spares. When
a failure occurs, the faulted disk is automatically swapped for a spare, and the
rocess of resynchronizing the array begins immediately. Where supported, hot
spares should be used as a master of course.

# Drawbacks of RAID 5

RAID 5 is a popular configuration, but it has some weaknesses, the following
issues apply to RAID 6 also, but for simplicity we frame the discussion in terms of
RAID 5.

First, it's critically important to note that RAID 5 does not replace regular off-line
backups. It protects the system against the failure of one disk—that it does not
protect against accidental deletion of files. It does not protect control-
liers, failures, hackers, or any of other hazards.

Second, RAID 5 isn't known for its great write performance. RAID 5 writes data
blocks to N-1 disks and parity blocks to the Nth disk.14 When a random block

Parity data is distributed all the drives in the array; each stripe has its parity stored on a differ-
ent drive. Since there's no dedicated parity disk, it's unlikely that any single disk will act as a bottleneck.

Chapter 10, Back-
ups, for general advice
ab backing up the
system.

![](bbox=[0.95, 0.447, 0.99, 0.547])