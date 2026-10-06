The following illustration shows the relationship between disks, physical volumes
(PVs), volume groups (VGs), and logical volumes (LVs) in LVM:

![](bbox=[0.264, 0.163, 0.735, 0.38])

STEP A:
Prepare the storage pool.
consists of three different hard disks.

32GB SCSI disk

160GB IDE disk

64GB SATA disk

STEP B:
Create a volume group by assigning disks
from your storage pool (Step A) to a volume
group. Assuming we use physical extents
(PEs) that are 32MB each, then:
SCSI disk = PV-1 = 32GB = 1000 PE
IDE disk = PV-2 = 160GB = 5000 PE
ATA disk = PV-3 = 64GB = 2000 PE
Therefore, there are a total of 87000 PEs
(or ~224GB) available to the volume group.

![](bbox=[0.274, 0.415, 0.461, 0.59])

PV-1
PV-2
PV-3

Volume Group 1

STEP C:
Create logical volumes (LVs) by using free
space from the parent volume group from
Step B.

+   1. Create an LV called LV-1, format it, and mount
its system on the /home directory. The LV
has been created with 3125 logical extents (or
100GB).
2. Create another LV called LV-2, format it, and
mount it at the /var directory. it has been
created with 62 logical extents (or 2GB).

![](bbox=[0.198, 0.693, 0.401, 0.833])

/var

Mount point for logical volume
/dev/volume-group-1/LV-2

/home

Mount point for logical volume
/dev/volume-group-1/LV-1