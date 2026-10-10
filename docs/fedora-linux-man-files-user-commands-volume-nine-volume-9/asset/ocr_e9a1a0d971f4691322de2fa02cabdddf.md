securely erased using a program like shred, though even this is ineffective with many modern storage technologies.

Use of qcow / qcow2 encryption is thus strongly discouraged. Users are recommended to use an alternative encryption technology such as the Linux dm-crypt / LUKS system.

cluster_size Changes the qcow2 cluster size (st be between 512 and 2M). Smaller cluster sizes can improve the image file size whereas larger cluster sizes generally provide better performance. preallocation Preallocation mode (allowed values: off, tadata, fallac, full). An image with preallocated tad data is initially larger but can improve performance when the image needs to grow. fullloc and full preallocations are like the sa options of raw format, but sets up tadata also. lazy_refcounts If this option is set to on, reference count updates are postponed with the goal of avoiding tadata I/O and improving performance. This is particularly interesting with cache=writethrough which doesn't batch tadata updates. The tradeoff is that after a host crash, the reference count tables st be rebuilt, i.e. on the next open an (automatic) qe-img check -r all is required, which may take so ti.

This option can only be enabled if compat=1.1 is specified.

nocow If this option is set to on, it will turn off cow of the file. It’s only valid on btrfs, no effect on other file systems.

Btrfs has low performance when hosting a vm image file, even more when the guest on the vm also using btrfs as file system. Turning off cow is a way to mitigate this bad performance. Generally there are two ways to turn off cow on btrfs: a) Disable it by mounting with nodatacow, then all newly created files will be NOCOW. b) For an empty file, add the NOCOW file attribute. That’s what this option does.

Note: this option is only valid to new or empty files. If there is an existing file which is cow and has data blocks already, it couldn’t be changed to nocow by setting nocow=on. One can issue lsattr filena to check if the NOCOW flag is set or not (Capital ‘C’ is NOCOW flag).

**Other** qemu also supports various other image file formats for compatibility with older QEMU versions or other hypervisors, including VMIDK, VDI, VHD (vpc), VHDX, qcowl and qbd. For a full list of supported formats see qe-img --help. For a more detailed description of these formats, see the qemu Elation User Documentation.

The main purpose of the block drivers for these formats is image conversion. For running VMs, it is recommended to convert the disk images to either raw or qcow2 in order to achieve good performance.