# 774 CHAPTER 22 NFS: SHARING FILESYSTEMS

# # INTRODUCTION TO NFS

Figure 22-1 shows the flow of data in a typical NFS client/server setup. An NFS directory hierarchy appears to users and application programs as just another directory hierarchy. By looking at it, you cannot tell that a directory holds a remotely mounted NFS directory hierarchy and not a local filesystem. The NFS server translates commands from the client to operations on the server's filesystem.

Diskless systems In many computer facilities, files are stored on a central fileserver equipped with large-capacity disk drives and devices that quickly and easily make backup copies of the data. A diskless system boots from a server (netboots—discussed next) or a CD/CDVD and loads system from a fileserver. The Linux Terminal Server Project (LTSP.org) Web site says all: "Linux makes a great platform for deploying diskless workstations that from a network server. The LTSP is also about running client computers in a diskless system does not require a lot of computing power, you can give older, retired computers a second life by using them as diskless systems.

Netboot/PXE You can netboot (page 1161) systems that are properly set up. Ubuntu Linux includes the PXE (Preboot Execution Environment; pxe package) server for netbooting Intel. Other systems sometimes use ftp (Trivial File Transfer Protocol; ftp and tftp packages) for netbooting. Non-Intel architectures have historically netboot capabilities, and Ubuntu Linux supports them. In addition, you can build the Linux kernel (/) using the many ways to set up a system, the one you choose depends on what you want to do. See the Remote-Boot mini-HOWTO for more information.

Dataless systems Another type of linux is a diskless system, when the client has no stored data (only Linux and the files are on the disk). Setting up this type of system is a matter of choosing directory hierarchies and remotely mounted.

df: where shows directory hierarchies The utility displays a list of directory hierarchies available on the system, along with the disk space, free and used, on each. The -h (human) option makes the output more intelligible. Device names in the left column are prepended with hostname: specifies filesystems that are available through NFS.

```
zach@plum:~ $ cd pwd
/dog.home/zach
z@plum:~ $ df -h
```

| Filesystem | Size Avail Use% Mounted on |
| /dev/sda1 | 28G 220M 26G 1% /home |
| /dev/sda2 | 9.2G 150M 8.6G 2% /p15 |
| /dev/sda5 | 1.4G 35M 1.3G 3% /p16 |
| dog:/home/zach | 19G 6.7G 11G 39% /dog.home/zach |
| grape/gc1 | 985M 92M 844M 10% /grape.gc1 |
| grape/gc5 | 3.9G 3.0G 738M 81% /grape.gc5 |