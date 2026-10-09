deploying diskless workstations that boot from a network server. The LTSP is all about running thin client computers in a Linux environment," Because a diskless workstation does not require a lot of computing power, you can give older, retired computers a second life by using them as diskless systems.

**Netboot/PXE** You can *netboot* (page 1262) systems that are appropriately set up. Fedora/RHEL includes **TFTP** (Trivial File Transfer Protocol); **tftp-server** package). You can use to set up a PXE (Preboot Execution Environment) boot server for Intel systems. Non-Intel architectures have historically included netboot capabilities, which Fedora/RHEL also supports. In addition, you can build the Linux kernel so it mounts **root** (/) using NFS. Given the many ways to set up a system, the one you choose depends on what you want to do. See the *Remote-Boot mini-HOWTO* for more information.

**Dataless systems** Another type of Linux system is a *dataless* system, in which the client has a disk but stores no user data (only Linux and the applications are kept on the disk). Setting up this type of system is a matter of choosing which directory hierarchies are mounted remotely.

> **df**: shows where directory hierarchies are mounted

The **df** utility displays a list of the directory hierarchies available on the system, along with the amount of disk space, free and used, on each. The **-h** (human) option makes the output more intelligible. Device names in the left column that are preped with *hostname*: specify directory hierarchies that are available through NFS.

```
[zach@guava ~]$ cd; pwd

[zach@guava ~]$ df -h
           Filesystem     Size Used Avail Use% Mounted on
/dev/mapper/fedora-root   37G  3.8G   32G  11% /
...
      /dev/sda1         477M   99M  354M  22% /boot
           plum:/home/zach   37G  3.8G   32G  11% /home/zach
```

When Zach logs in on *guava*, his home directory, **/home/zach**, is on the remote system *plum*. Using NFS, the **/home/zach** directory hierarchy on *plum* is mounted on *guava* as **/home/zach**. Any files in the *zach* directory on *guava* are hidden while the *zach* directory from *plum* is mounted; they reappear when the directory is unmounted. The / filesystem is local to *guava*.

The **df** -T option adds a Type column to the display. The following output shows the directory mounted at **/home/zach** is an **nfs4** directory hierarchy; **/** and **/boot** are local ext4 filesystems.

```
$ df -hT
           Filesystem     Type     Size Used Avail Use% Mounted on
/dev/mapper/fedora-root ext4      37G  3.8G   32G  11% /
...
      /dev/sda1         ext4      477M   99M  354M  22% /boot
           plum:/home/zach      nfs4     37G  3.8G   32G  11% /home/zach
```

The **df** -t option displays a single filesystem type. With an argument of **nfs4** it displays NFS directory hierarchies: