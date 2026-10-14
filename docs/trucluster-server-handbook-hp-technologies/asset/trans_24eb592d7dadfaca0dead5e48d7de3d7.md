
resources, testing, 792
setup resources, 747
setup window, 746
single-instance applications and, 670
start resources informational popup, 749
with sysman, 745–50
uses, 672
Cluster-aware applications, 27–28
Cluster-common disk(s), 387
adding, to LSM, 388
adding, to root disk group, 388
Cluster-common files, 145, 310
differentiating, 146–48
location, 145
rc.config.common, 146, 151, 606, 607
Cluster-common file system
migrating, 386–91
rules and restrictions, 367
Cluster configuration planning, 57–110
checklist, 107–9
CI hardware, 88–101
console level preparation, 102–6
disk devices, 57–85
failure, 57
firmware, 85–88
future expansion, 76
hardware RAID, 72–81
hardware storage, 65–72
licensing requirements, 106
network, 106–7
swap areas, 63–64
Tru64 UNIX system disk, 58–63
Cluster design, 35–55
applications and, 37–43
availability and, 43–44
CLUA common-subnet alias and, 50
computing resources, 41
default options, 35–36
example, 36–37
Fibre Channel based storage, 36
hardware RAID/LVM decision, 53–54
homogeneity of members, 36
independent paths and, 55
introduction to, 35–37
network interfaces and, 49
parallel applications and, 39–40
quorum disk and, 45–46
redundant Memory Channel, 36
redundant NICs, 36
scalability and, 44–45
size, 36
storage configuration, 52–53
tradeoffs, 35
Cluster File System (CFS), 23, 29, 327–57
block I/O and, 418
boot error (mounting boot partition), 810
boot error (mounting cluster_root), 810
capacity issues, 351
checking, 278
common code and, 581
defined, 29, 327
events, 357
file system support, 331–32
I/O requests to DRD, 431
load balancing, 348–51
memory usage, 352–54
performance optimizations, 348–57
POSIX compliance, 555
read-ahead thread, 355–57
relationships, 29
write-behind thread, 355–57
See also CFS clients; CFS server
Cluster formation, 507–10
details, 507–10
process, 507
transaction, 510
without enough votes, 540–41
See also Connection Manager (CNX)
Cluster interconnect (CI), 25, 46–49
as cluster design decision, 46–48
cluster IP name/address determination, 100
comparison, 48, 101
dual-redundant, 48–49
functions, 89
hardware, configuring/verifying, 88–101
IP address, 262
IP name, 261–62
LAN-based, 46, 47, 98–100
Memory Channel, 46, 47, 90–97
as migration issue, 786
role of, 46–47
types, 46
types, entering, 262–64, 287–89
virtual address, 600
Cluster Logical Storage Manager (CLSM), 359–402
defined, 359
disk group connectivity, 367
events, 402
location, 359
notes, rules, and restrictions, 365–67
See also Logical Storage Manager (LSM)
Cluster members
adding, 44–45, 283–93151
adding, one at a time, 282
add preparation, 282
boot device, identifying, 294
boot disk, 81, 261
booting, 293–96
boot_partition, 282, 285–86
in CFS server, 329–30
communication between, 24
configuring, 296–98
deleting, 282, 302–6
file system use determination, 350–51
homogeneity of, 36
IDs, 146, 260
interconnect address, changing, 668
IP address, changing, 668
lead, determining, 756–57
lead, reboot, 770
locking, 89
memberid, 284
multiple network interfaces, 32
name, changing, 668
new, boot disk, 282
old, adding to cluster, 794–95
planning, 282
potential, in cluster formation, 508
qdisk thread, 525
rebooting, 400
resource run determination on, 710
retrieving events from, 321
rolling, 773–78
rolling, after dupatch program, 777
rolling, after installupdate program, 774–77
scalability, 45
shared storage view, troubleshooting, 806–8
single, multiple applications on, 42–43
specific files, 145
systems, homogeneity, 43
UNIX kernel building for, 296
verifying, 299–301
as VLM systems, 64
votes, adjusting, 518–20
See also Clusters
Cluster Mount Services (CMS), 567
defined, 567
output, 567
Cluster partition, 498–500
defined, 498
illustrated, 500
panic strings, 499
sizes, 248
cluster_root
backup, 637
checking, 590
copying updated cluster database files to, 644
device name determination, 638
disk partitioning, 638
domain creation, 641
expanding, 589
major/minor numbers, 640, 645
mounting, 639, 641
mounting, CFS boot error, 810
repairing, 592
restoring, 637–45
restoring, to existing disk, 637–40
restoring, to new disk, 640–45
verify utility and, 592
Clusters
