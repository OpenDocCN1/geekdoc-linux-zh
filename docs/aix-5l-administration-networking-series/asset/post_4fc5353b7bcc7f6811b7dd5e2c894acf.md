
Next we need to list the adapter locations within the system:

```bash
# lsdev -Cc adapter | grep scsi

  scsi0  Available  04-B0  Wide SCSI I/O Controller
  scsi1  Available  04-03  Wide SCSI I/O Controller
```

We now need a list of the volume groups involved in this disk reassignment:

```bash
# lspv

  hdisk0    000400434b33e6eb    rootvg
  hdisk1    000400434a771e22    rootvg
  hdisk2    000400439e42cd74    appvg
  hdisk3    000400439a5def f0    appvg
  hdisk4    000400439ae07e9    appvg
```

Before we make any changes, we first need to make the target volume group unavailable:

```bash
# varyoffvg appvg
```

> See the section "Varying On and Varying Off Volume Groups" later in this chapter for more details.

Now we can remove the target devices on **scsi1 (2@8,0 3@8,0 4@0,0)**. From the command prompt, enter the following command sequence. Basically, this is like writing a shell script on the command line:

```bash
# for N in 2 3 4
> do
> rmdev -dl hdisk$N
> done
```

> **NOTE** Do not type the greater than signs (>), because these are prompts. Press ENTER after each line.

Preview the commands to add the devices with new names:

```bash
# for NA in 10@8,0 12@9,0 14@10,0
> do
> N=$(echo $NA | awk -F@ '{print $1}')
> A=$(echo $NA | awk -F@ '{print $2}')
> echo "mkdev -c disk -s scsi -t oadisk -p scsi1 -w $A -l hdisk$N -a pv=yes"
> done
```

The preview output will show these commands:

```bash
mkdev -c disk -s scsi -t oadisk -p scsi1 -w 8,0 -l hdisk10 -a pv=yes
mkdev -c disk -s scsi -t oadisk -p scsi1 -w 9,0 -l hdisk12 -a pv=yes
mkdev -c disk -s scsi -t oadisk -p scsi1 -w 10,0 -l hdisk14 -a pv=yes
```

Now remove the **echo** around the **mkdev** command to actually execute the commands:

```bash
# for NA in 10@8,0 12@9,0 14@10,0
> do
> N=$(echo $NA | awk -F@ '{print $1}')
> A=$(echo $NA | awk -F@ '{print $2}')
> mkdev -c disk -s scsi -t oadisk -p scsi1 -w $A -l hdisk$N -a pv=yes
> done
```

The resulting output is shown here with our new hdisk numbers:

```bash
hdisk10 Available
hdisk12 Available
hdisk14 Available
```

List the new device names:

```bash
# lsdev -Cc disk

hdisk0 Available 04-B0-00-0,0 Other SCSI Disk Drive
hdisk1 Available 04-B0-00-1,0 Other SCSI Disk Drive
hdisk10 Available 04-03-00-8,0 Other SCSI Disk Drive
hdisk12 Available 04-03-00-9,0 Other SCSI Disk Drive
hdisk14 Available 04-03-00-10,0 Other SCSI Disk Drive
```

List the hdisks numbers, PVIDs, and the associated volume groups:

```bash
# lsvg

hdisk0 0004040434b32e6eb rootvg
hdisk1 0004040434a781e22 rootvg
hdisk10 0004040439e42cd74 appvg
hdisk12 0004040439a5def0 appvg
hdisk14 0004040439a5e07e9 appvg
```

Note that the physical disks in a volume group are identified by the PVID and not by the hdisk number. We do not have to import the volume group again before we vary it on.

```bash
# lqueryvg -Atp hdisk10

Max LVs:              256
PP Size:              25
Free PPs:             504
LV count:             3
PV count:             3
Total VGDAs:          3
Conc allowed:         0
MAX PPs per PV:       1016
MAX PVs:              32
Conc Autovar:         0
Varied on:            0
Logical:
      000400439a5df5d2.1   lv1ac1 1
      000400439a5df5d2.2   lcg1v00 1
      000400439a5df5d2.3   lv01 1
Physical:
      000400439a5d5eff 1    0
      000400439a5e07e9 1    0
      000400439e42cd74 1    0
Total PPs:            813
```

Make the volume group available again by varying **appvg** back online:

```bash
# varyonvg appvg     No need for importvg in this case
```

## Configuring a Hot Spare

In this hot spare example, **appvg** is mirrored from hdisk1 to hdisk2, and hdisk3 and hdisk4 will be the hot spares:

```bash
# lsvg appvg
VOLUME GROUP:   appvg                  VG IDENTIFIER: 0000224800004900000000000ebab4a5fe2
VG STATE:       active                PP SIZE:        32 megabyte(s)
VG PERMISSION:  read/write            TOTAL PPs:      2184 (69888 megabytes)
MAX LVs:        256                   FREE PPs:       2184 (69888 megabytes)
LVs:            0                     USED PPs:       1092 (34944 megabytes)
OPEN LVs:       0                     QUORUM:         1
TOTAL PVs:      4                    VG DESCRIPTORS: 3
STALE PVs:      0                    STALE PPs:      0
ACTIVE PVs:     4                    AUTO ON:        yes
MAX PPs per PV:  1016         MAX PVs:              32
LTG size:        128 kilobyte(s)  AUTO SYNC:          no
HOT SPARE:       no
```

Check for the volume groups associated with the disks:

```bash
# lsvpv
hdisk0        0000468644af1894        rootvg
hdisk1        00003095a330a867        appvg
hdisk2        00003095a330baa8        appvg
hdisk3        00003095a330bca2        appvg
hdisk4        00003095a330c825        appvg
```

The **chpv** command has a **-h** flag that sets the characteristics and the allocation permissions of the physical volume so that it can be used as a hot spare. The **-h** flag has no effect for nonmirrored logical volumes. The **-h** flag can take either **y** or **n** as a parameter to add or remove the disk to or from the hot spare pool.

Set up the hot spare disks:

```bash
# chpv -h 'y' hdisk3 hdisk4    # -h [y|n]
```

Check the hot spare disks:

```bash
# for N in a867 baa8 bca2 c825
> do
> lquerypv -g 000022480004a900000000bab4aeefe2 -P 00003095a330$N -S
> done
0
0
32
32
```

> **NOTE** Do not enter the greater-than (>) signs; these are prompts.

Just like the **chpv** command, the **chvg** command uses the **-h** flag to set the sparing characteristics for the volume group, which is specified by the VolumeGroup parameter. The **-h** flag has four parameters that may be used:

-   **y**    Allows for automatic migration of failed disk partitions from one failed disk to one hot spare.
-   **Y**    Allows for automatic migration of failed disks and can migrate to the entire hot spare pool. This is different than a one-to-one partition migration.
-   **n**    Prohibits failed disk migration. This is the default.
-   **r**    Removes all of the disks from the hot spare pool for the volume group.

Next we will enable a hot spare for the volume group:

```bash
# chvg -h 'y' -s 'y' appvg
```

We use the **s** flag to sync the mirrors in the previous command.

View the volume group changes:

```bash
# lsvg appvg
VOLUME GROUP:      appvg      VG IDENTIFIER:
000022488000004900000000ebab4ae6f2
VG STATE:          active     PP SIZE:      32 megabyte(s)
VG PERMISSION:     read/write TOTAL PPs:    2184 (69888 megabytes)
MAX LVs:           256        FREE PPs:     2184 (69888 megabytes)
LVs:               0          USED PPs:     1092 (34944 megabytes)
OPEN LVs:          0          QUORUM:       1
TOTAL PVs:         4          VG DESCRIPTORS: 3
STALE PVs:         0          STALE PPs:    0
ACTIVE PVs:        4          AUTO ON:      yes
MAX PPs per PV:    1016      MAX PVs:      32
LTTG size:         128 kilobyte(s) AUTO SYNC:    yes
HOT SPARE:         yes (one to one)
```

Check for errors:

```bash
# errpt | head -3
IDENTIFIER TIMESTAMP  T C RESOURCE_NAME  DESCRIPTION
A60F45A8 0127191502 I O RMCDaemon The daemon is started.
7F88E76D 0127184302 P S console SOFTWARE PROGRAM ERROR
```

Check the daemon:

```bash
# lssrc -s ctrmc
Subsystem     Group         PID   Status
ctrmc         rstart        13934 active
```

Check the process tree:

```bash
# pstree -p 13934
+- 00001 root /etc/init
|+- 03150 root /usr/sbin/srcmstr
\-+- 13934 root [3]/usr/sbin/rscd/bin/rscmd -c
```

Or just use the AIX ps command:

```bash
# ps -ef | grep rscmd
root 13934 3150 0 10:02:00 - 0:00 /usr/sbin/rscd/bin/rscmd -c
```

If you like using the **pstree** freeware program, you can get the source code at either of the following URLs:

```
http://freshmeat.net/projects/pstree/
ftp://ftp.thp.Uni-Duisburg.DE/pub/source/
```

## INTRODUCING THE LVM

If you plan to work with AIX, you *must* learn and understand the Logical Volume Manager (LVM) and how it works. I want to start with the makeup of the LVM. We start with the largest structure, which is one or more disks grouped together to make a *volume group (VG)*. Within the VG, we create *logical volumes (LVs)*. The LV is made up of *logical partitions (LPs)* that are mapped to actual disk partitions called *physical partitions (PPs)*. On top of the LV, we can create *filesystems*, which have a mount point or directory. We can also have *raw logical volumes*, which are nothing more than an LV without a mount point that is accessed through its raw device name. Databases like to use raw LVs, but it is a big no-no to pair raw LVs with High Availability Cluster Multi-Processing (HACMP)! For details on HACMP, see Chapter 28.

The LVM consists of the following components:

-   Volume groups (VGs)
-   Physical volumes (PVs)
-   Logical volumes (LVs)
-   Logical partitions (LPs)
-   Physical partitions (PPs)

Notice the acronyms for each component: VG, PV, LV, LP, and PP. You will see these often, so please learn each acronym. If you understand the concepts of the preceding five LVM components and how they interrelate, you have it licked. We are going to take these components one at a time and explain how they interrelate.

A *physical partition* (*PP*) is a section of disk space that can be used for *logical volumes (LVs)*. Typically, logical volumes are for filesystems and for paging space. Traditional legacy UNIX systems restrict partitions to contiguous space on a single disk such that a single filesystem cannot be any larger than the size of available contiguous space on a single disk. However, AIX uses the concept of *logical volumes (LVs)* to map to physical disk space. A logical volume is represented by a mapping of *logical partitions* (*LPs*) to *physical partitions (PPs)* residing on *one or more physical disks* within the same *volume group (VG)*.

Each physical disk may contain up to 1016 physical partitions (PPs) ranging in size from 1 to 256 megabytes, in powers of 2. Starting in AIX 4.3, you can increase the number of PPs, but you will decrease the maximum number of disks for the VG. There are mathematical limits to addressing that require this give and take. The default
