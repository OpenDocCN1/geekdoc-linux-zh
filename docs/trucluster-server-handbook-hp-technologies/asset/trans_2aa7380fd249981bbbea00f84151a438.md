
alias IP address, 258
alias name, 258
backing up, 757
BIND in, 602
checking, with hwmgx (8)
command, 272
chronology, 6
as closely coupled, 21–22
configuration, checking, 270–72
configuring, 266–69, 291–93
coupling, 22
creating, 790–91
defined, 1–2, 23
DHCP in, 602–3
Disaster Tolerant (DT), 8
disks for, 246–49
distributed computing vs., 2
failover cluster, 2
firmware for, 85–88
heterogeneous, 43
homogeneous, 43
hung, 799–800
installation, before, 245–50
interconnect, 24
IP address, 287
IP address, changing, 667–68
IP name, 286
joining, 510–13
LSM, 31
maintenance and recovery, 635–68
name, changing, 666–67
network planning, 106
NFS in, 603–9
NIS in, 609
preparation checklist, 107–9
single-node, creating, 245–79
SSI application, 2, 3
SSI systems, 2, 3–4
stretch, 8
subsystem components, 34
system administration in, 571–73
two-member, 22
UNIX, 2
upgrade determination, 759
V1.56, 796–97
VAXCluster, 4
verification, 272–79

See also Cluster members
Cluster's Expected Votes (CEV), 496–97, 513
adjusting, 520–22
defined, 496–97
recalculation, 498
Cluster system block (CSB), 490–92
defined, 490
events stored in, 491
list of, 491
cluster_usr, 639, 642
domain creation, 641
restoring, 639, 642
cluster_var
domain creation, 641
restoring, 639, 642
Cluster-wide device naming, 403–4
Cluster-wide files, 580–87
directories, 581
fstab, 580
group, 580
inittab, 582–83
passwd, 580
rc.config scripts, 583–84
sysconfigtab, 584–87
system startup, 582–87
vmunix, 581–82
Cluster-wide I/O, 405–8
clu_upgrade command
clean option, 779
roll option, 773–74
setup option, 761
switch option, 778
-v check setup option, 760
-v status option, 779–80
cnx partition, 493, 530–37
AdvFS cluster_root devices
segment, 535–36
CLSM cluster_root devices
segment, 536–37
configuration, 531
configuration information storage, 531
contents, 532–37
information, retrieving, 530
information display, 493

Context-Dependent Symbolic Links
(CDSLs), 145, 146, 158–63, 310–13, 582
additional, since cluster creation, 311
broken, repairing, 313
cdslinvchk(8) command and, 159–60
creation, 267
defined, 147
exporting file systems containing, 605–6
maintaining, 159–62
mkcdsl(8) command and, 158–59
mv(1) command and, 162, 312–13
public service announcement, 158
removing, 160, 313
resolved, 147
root (/) directory, 156
shells and, 162–63
/usr directory, 157
/var directory, 157
cp(1) command, 162, 312, 652
CPU
defined, 17
multiple, systems, 19–20
single, computer, 17–19
crashdc(8) command, 581
Crash files, 800
cron(8) daemon, 627–28
crontab file, 627, 706
C shell, 162
csh shell, 162, 163
csid, 492
Customer Specific Patches (CSPs)
defined, 651
installing, 651–52
cut(1) command, 171

dcc d.dat file, 173
dd command, 415, 419
ddr.db, 174
dec_cdb, 174
dec_devsw_db, 174
dec_hwc_1db, 174–75
dec_hw_db, 174
DECSafe ASE, 4
dec_scs i_db, 175
dec_unid_db, 175–76
Deleting cluster members, 302–6
with clu_delete_member command, 302–6
completion, 306
one at a time, 282
steps for, 303–4
See also Cluster members
Dependent resources, 730–31
devAPP application resource, 742–43
/dev directory, reinitializing, 193–94
Device Request Dispatcher (DRD), 30, 403–32
access member name, changing, 410–12
checking, 276–77
concepts, 403–10
configuring, 410–15
defined, 30, 403
events, 432
by example, 415–32
handling requests, 30
information on, 277
I/Os returned to, 409
looking for devices, 404
path failure response, 426–32
relationships, 30
rerouting of I/O, 55
statistics, 419
statistics, querying, 422
Devices
checking paths to, 421
cluster-wide naming, 403–4
DAIO, 349, 406–8
DRD looking for, 404
I/O subsystem relationship, 361
served, 408, 413–14, 422–26
statistics, resetting, 414
viewing, 314
/devices directory, reinitializing, 193–94
Device Special File Manager. See dsfmgr command

Device special files
block, 418
checking, for inconsistencies, 194
creating, for new device, 189
databases, error-free verification, 192
errors, repairing, 192–93
EVM, 196
exchanging, 191
information, viewing, 189
location of, 168
naming conventions, 168
renaming, 189
tape, creating from installation CD, 194
df(1) command, 333
dfsc.dat file, 176–77
dfsl.dat file, 176–77
diff(1) command, 316, 502
DIOMAP tokens, 341
Direct Access Cached Reads, 346–47, 355
enabling, 347
illustrated, 347
non physical connection, 347
Direct-Access I/O (DAIO) devices, 349, 406–8
illustrated, 407
on private bus, 407
on private-bus examples, 420–22
on semi-shared bus, 411
on shared bus examples, 415–20
Direct I/O, 328, 345–46
Concurrent, 328, 346
enabling, 345
illustrated, 345
information on, 346
I/O flows with, 345
Disaster Tolerant (DT) clusters, 8
diskconfig(8) command, 62, 63
Disk Configuration application, 61–62
Disk groups, 366
connectivity, 367
deporting, from LSM, 376, 378
identifier (DGID), 377
importing, 374–81
importing, from cluster to cluster, 380–81
importing, from cluster to standalone system, 379–80
importing, from standalone system to cluster, 376–79
removing disks from, 396–97
volumes, initializing, 380
volumes, starting, 380
disklabel(8) command
checking disk label with, 369
partitioning with, 60–61
Disk labels
checking, 369
editing, 397, 400–401
replacing, 397
saving, 387, 397, 631
Disk partitions
encapsulating, 394
layout, 122
selections, verifying, 126
standalone layout, 126
unencapsulating, 398
Disk(s)
adding, to LSM, 387
for cluster, 246–49
cluster-common, 387
disklabel, editing, 249
Emergency Repair (ER), 645
encapsulating, 381–82, 394
"hot spare," 640
minimum configuration, 52
physical, 362
removing, from disk group, 396–97
requirement, 246–49
swap, 400
system, 78–80, 122
unencapsulating, 398
Distributed Lock Manager (DLM), 26, 27–28, 89, 555–60
cluster subsystem communication, 560
as cluster-wide mechanism, 28
for cluster-wide synchronization, 558
in component hierarchy, 559
create a lock, 557
