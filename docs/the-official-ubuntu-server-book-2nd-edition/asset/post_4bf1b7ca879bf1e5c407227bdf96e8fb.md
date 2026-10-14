
MD (multidisk) devices, 342
migrating from RAID 1 to RAID 5, 351–354, 356–357
migrating non-RAID disks to RAID, 347, 350
/opt directory, 6
partitions, definition, 5–6
partitions, maximum per disk, 10
for personal files for user accounts, 6
for RAID devices, 338–340, 341
resizing current partitions, 8
for temporary files, 7
for third-party programs, 6
/tmp directory, 7
/usr directory, 7
/var directory, 6
for variable-size data, 6
Disk partitioning, manual
allocating free space, 9–10
boot flag, setting, 13
"Bootable flag" field, 13
extended partitions, 10
file system, specifying, 10
file system settings, 10, 13
initializing a blank drive, 9
inodes, setting number of, 12
inside extended partitions, 10
"Label" field, 12
logical partitions, 10
mount options, 11
"Mount options" field, 11
mount point, specifying, 11
"Mount point" field, 11
naming partitions, 12
partition size, specifying, 10
partitions as physical volumes, 10
primary partitions, 10
"Reserved blocks" field, 12
reserving space for the superuser, 12
"Typical usage" field, 12
"Use as" field, 10–11
Disk partitioning, preseeding
custom schemes, 92–94
expert_recipe for, 92–94
formatting partitions, 94
LVM partitions, 95–96
maximal size, 93
minimal size, specifying, 93
mountpoint, specifying, 94
overview, 91
partman-auto/choose_recipe option, 92
partman-auto/method option, 91
partman-auto/purge_lvm_from_device option, 91–92
partman/choose_partition option, 92
partman/confirm_option, 92
partman/confirm_write_new_label option, 92
partman-lvm/confirm_option, 91–92
primary partition, 94
priority, specifying, 93–94
warning prompts, disabling, 91
Disk space
allocating, 9–10
freeing, rescue and recovery, 423
reserving for the superuser, 12
Disk space, troubleshooting
df command, 405–407
du command, 406–407
excessive tmp files, 407
full file system, 407
out of inodes, 407–408
usage, by directory, 406–407
usage, by file system, 406–407
Diskless clients, 180
Disks. See also Hard drives.
erasing, 478
failure, automatic notification, 345. See also Hard drives, rescue and recovery.
images, restoring from, 241
I/O, monitoring, 270
management, drbdadm command, 387–389
snapshots of, 8
DISPLAY option, 193
Distributions
definition, 53
specifying, 78
Dividing the problem space, 392–393
DNS (Domain Name System)
address, specifying, 306
status, checking, 412–413
ufw firewall example, 221
--dns option, 306
DNS queries, dig tool, 483–484
DNS servers
caching name server, 129
definition, 13
DNS master, 129–132
DNS slave, 132–133
host e-mail address, specifying, 130
overview, 126–127
SOA (Start of Authority), specifying, 130
TTL (Time To Live), default setting, 130
DNS servers, BIND
configuration files, reloading, 134
current status, checking, 134
default log file, 129
documentation, 134
/etc/bind/, 128
/etc/bind/db.*, 128
/etc/bind/named.conf, 128
/etc/init.d/bind9, 128
file conventions, 127–129
flush command, 134
init script, location, 128
installing, 127
managing with rndc, 134
as name server, 127
named.conf file, 128
reconfig command, 134
reload command, 134
retransfer zone command, 134
server caches, flushing, 134
slave zone files, location, 128
status command, 134
/var/cache/bind, 128
/var/log/syslog, 129
working directory, 128
zones, reloading, 134
DNS servers, BIND zone files
adding, 129–132
location, 128
ownership, 131
permissions, 131
referencing in named.conf, 131–132
reloading, 134
retransferring, 134
DNS slave server
configuring the master server, 132–133
configuring the slave server, 133
overview, 132
Document root directory, 139
Documentation. See also Help and resources.
Apache Web server, 141
DNS servers, BIND, 134
doc files, 450
expert_recipe partitioning, 92–94
GroundWork front end, 294
GRUB boot loader, 25
installation CDs, 4
localhost, 449–450
man command, 22
man pages, 449–450
mdadm tool, 346
online, 448
packages, 54–55
sudoers file, 204
troubleshooting problems and solutions, 394–395
Domain default, specifying, 305
Domain name for sent mail, 152
Domain Name System (DNS). See DNS (Domain Name System).
--domain option, 305
Domains, accepting mail from, 152
do-release-upgrade program, 76
Dot (.)
alias for current directory, 20
package paragraph separator, 62–63
partition separator, 94, 96
Dot dot (..), alias for directory above current, 20
Dovecot, 157–158
Downloading packages automatically, 65
dpkg option, 423
dpkg program
copying packages to another system, 77
file owner package, identifying, 71
listing installed packages, 76–77
listing package files, 70–71
manipulating installed packages, 69–71
mirroring a system, 76–77
overview, 55, 69
querying installed packages, 69–71
searching installed packages, 69–71
