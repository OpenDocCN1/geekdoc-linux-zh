# Chapter 8 Storage

# Resizing filesystems

Filesystem overflows are more common than disk crashes, and one advantage of logical volumes is that they are much easier to juggle and resize than are hard partitions. We have experienced everything from servers used for personal MP3 stores to a department full of email pack rats.

The logical manager doesn't know anything about the contents of its volumes, so you must resize it at both the volume and filesystem levels. The order depends on the specific operation. Reductions must be filesystem-first, and enlargements must be volume-first. Don't memorize these rules: just think about what's actually happening and use common sense.

Suppose that in our example, /mnt/web1 has grown more than we predicted and needs another 10GB of space. We first check the volume group to ensure additional space is available.

```
$ vgdisplay DEMO
--- Volume group ---
VG Name DEMO
System ID
Format svm2
Metadata Areas 1
Metadata Sequence No 18
VG Access read/write
VG Status resizable
MAX LV 0
Cur LV 2
Open LV 1
Max PV 0
Cur PV 1
Act PV 1
VG Size 975.99 GB
PE Size 4.00 MB
Total PE 249854
Alloc PE / Size 51200 / 200.00 GB
Free PE / Size198654 / 775.99 GB
VG UUID NtRLu-RqiJ-3Urt-iQn-eVVj-u0Th-FVKYWF
```

Plenty of space is available, so we mount the filesystem and use Lversize to add space to the local volume.

```
$ sudo mount /mnt/web1
$ sudo lvechange -an DEMO/web1
$ sudo lveresize -L +10GB DEMO/web1
$ sudo lvechange -ay DEMO/web1
```

Extending logical volume web1 to 110.00 GB
Logical volume web1 successfully resized

The Lvechange commands are needed to deactivate the volume for resizing and to reactivate afterwards. This part is only needed because there is an existing snapshot-of web1 from our previous example. After the resize operation, the snapshot