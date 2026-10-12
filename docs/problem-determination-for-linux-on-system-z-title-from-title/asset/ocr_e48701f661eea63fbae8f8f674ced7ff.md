dasd(eckd): 0.0.3302: (4kB blks): 2404080kB at 48kB/trk compatable disk layout
dasdb:VOL1/ 0X3302: dasdb1
dasd(ckd): 0.0.3303: 3390/0A(CU:3990/01) Cyl:3339 Head:15 Sec:224
dasd(eckd): 0.0.3303: (4kB blks): 2404080kB at 48kB/trk compatable disk layout
dasc:VOL1/ 0X3303: dasdc1
dasd(eckd): 0.0.3304: 3390/0A(CU:3990/01) Cyl:3339 Head:15 Sec:224
dasd(eckd): 0.0.3304: (4kB blks): 2404080kB at 48kB/trk compatable disk layout
dasd:VOL1/ 0X3304: dasdd1
Waiting for /dev/mapper/control to appear:. . ok
Reading all physical volumes. This may take a while...
Found volume group "rootvg" using metadata type lvm2
1 logical volume(s) in volume group "rootvg" now active
kjournald starting. Commit interval 5 seconds
EXT3-fs: mounted filesystem with ordered data mode.
VFS: Mounted root (ext3 filesystem) readonly.
Trying to move old root to /initrd ... /initrd does not exist. Ignored.
Unmounting old root
Trying to free ramdisk memory ... failed
Freeing unused kernel memory: 116k freed

To a better understand this we spilt the message boot logs according to the topics below:

+   - Loading device driver (kernel boot phase - processing initrd)
+   Loading kernel/fs/jbd/jbd.ko
+   Loading kernel/fs/ext3/ext3.ko
+   Loading kernel/drivers/md/md-mod.ko
+   Loading kernel/drivers/md/dm-snapshot.ko
+   Loading kernel/drivers/s390/block/dasd_mod.ko dasd=3301-3304
+   Loading kernel/drivers/s390/block/dasd_eckd_mod.ko

+   - DASD recognition (kernel boot phase - processing initrd)
+   dasd(eckd): 0.0.3301: 3390/0A(CU:3990/01) Cyl:3339 Head:15 Sec:224
+   Using cfq io scheduler
+   dasd(eckd): 0.0.3301: (4kB blks): 2404080kB at 48kB/trk compatable disk layout
+   dasa:VOL1/ 0X3301: dasdala dasda2 dasda3
+   dasd(eckd): 0.0.3302: 3390/0A(CU:3990/01) Cyl:3339 Head:15 Sec:224
+   dasd(eckd): 0.0.3302: (4kB blks): 2404080kB at 48kB/trk compatable disk layout
+   dasdb:VOL1/ 0X3302: dasdb1
+   dasd(eckd): 0.0.3303: 3390/0A(CU:3990/01) Cyl:3339 Head:15 Sec:224