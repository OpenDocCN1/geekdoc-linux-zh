The main benefit of volume-groups is the abstraction between the logical- and physical-volumes. The VG takes the storage space from the PVs and divides it into fixed-size chunks called physical-extents (PEs). An LV is then created by assigning one or more PEs to the LV. This assignment can be done in any arbitrary orderthere is no dependence on the underlying order of the PVs, or on the order of the PEs on a particular PV. This allows LVs to be easily resized. If an LV needs to be expanded, any unused PE in the group can be assigned to the end of that LV. If an LV needs to be shrunk, the PEs assigned to the end of that LV are simply freed.

The volume-group itself is also easily resizeable. A new physical-volume can be added to the VG, and the storage space on that PV becomes new, unassigned physical-extents. These new PEs can then be used to expand existing LVs or to create new LVs. Also, a PV can be removed from the VG if none of its PEs are assigned to any LVs.

In addition to expanding and shrinking the LVs, data on the LVs can be "moved" around within the volume-group. This is done by reassigning an extent in the LV to a different, unused PE somewhere else in the VG. When this reassignment takes place, the data from the old PE is copied to the new PE, and the old PE is freed.

The PVs in a volume-group do not need to be individual disks. They can also be RAID volumes. This allows a user to get the benefit of both types of volume management. For instance, a user might create multiple RAID-5 volumes to provide data redundancy, and then use each of these RAID-5 volumes as a PV for a volume-group. Logical-volumes can then be created that span multiple RAID-5 volumes.

# ## Device Special Files

A typical Linux system has at least one hard disk, a keyboard, and a console. These devices are handled by their corresponding device drivers. However, how would a user-level application access the hardware device? Device special files are an interface provided by the operating system to applications to access the devices. These files are also called device nodes that reside in the /dev directory. The files contain a major and minor number pair that identifies the device they support. Device special files are like normal files with a name, ownership, and access permissions.

There are two kinds of device special files: block devices and character devices. Block devices allow block-level access to the data residing on the device, and character devices allow character-level access to the device. When you issue the `ls l` command on a device, if the returned permission string starts with a b, it is a block device; if it starts with a c, it is a character device.

# ## devfs

The virtual file system, devfs, manages the names of all the devices. devfs is an alternative to the special block and character device node that resides on the root file system. devfs reduces the system administrative task of creating device nodes