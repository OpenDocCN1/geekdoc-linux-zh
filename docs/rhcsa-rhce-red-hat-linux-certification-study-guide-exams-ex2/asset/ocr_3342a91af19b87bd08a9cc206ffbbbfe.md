| Volume Group Command | Description |
|---|---|
| vgextend | If you've created a new PV: vgextend vggroup00 /dev/sda11 adds the space from /dev/sda11 to vggroup00. |
| vgmerge | If you have an unused VG vggroup01, you can merge it into vggroup00 with the following command: vgmerge vggroup00 vggroup01. |
| vgmknodes | Run this command if you have a problem with VG device files. |
| vgreduce | The vgreduce vggroup00 /dev/sda11 command removes the /dev/sda11 PV from vggroup00, assuming sufficient free space is available. |
| vgremove | The vgremove vggroup00 command removes vggroup00, assuming it is not assigned to any LV. |
| vgrename | Allows renaming of LVs. |
| vgs | Displays basic information on configured VGs. |
| vgscan | Scans and displays basic information on configured VGs. |
| vgsplit | Splits a volume group. |

As you assign PVs to VGs and then subdivide VGs into LVs, you may need commands to control and configure them. Table 6-7 includes an overview of related LVM commands.

| Logical Volume Command | Description |
|---|---|
| lvchange | Similar to pvchange, changes the attributes of an LV: for example, the lvchange -an vggroup00/lvol00 command disables the use of the LV labeled lvol00. |
| lvconvert | If there are sufficient available PVs, the lvconvert -m1 vggroup00/lvol00 command mirrors the LV. |
| lvcreate | Creates a new LV in an existing VG. For example, lvcreate -L 200 volume01 -n lvol01 creates lvol01 from 200 extents in the VG named volume01. |
| lvdisplay | Displays currently configured LVs. |
| lvextend | Adds space to an LV: the lvextend -L4G /dev/volume01/lvol01 command extends lvol01 to 4GB, assuming space is available. |
| lvreduce | Reduces the size of an LV; if there's data in the reduced area, it is lost. |
| lvremove | Removes an active LV: the lvremove volume01/lvol01 command removes all lvol01 from VG volume01. |