
You should also familiarize yourself with the graphical OCFS2 frontend **ocfs2 console** which allows to administer different aspects of OCFS2.

![](img/63e88022bf135307e3eac051ad238b5b_443_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_443_1.png)

# OCFS to OCFS2 Migration

The on-disk layouts of OCFS and OCFS2 are not compatible. As drivers for OCFS only exist for 2.4.x linux kernels and drivers for OCFS2 only for 2.6.x linux kernels, you cannot use them both on the same machine concurrently.

There are two possibilities to migrate to the new OCFS2:

- If the old cluster file system is still online you can replicate it to the new one via the network. You have to ensure that there are no changes to the old OCFS storage cluster after the last replication; during the migration you need double SAN capacity.
- Oracle provides the FSCat tools that can read OCFS disk images in userland. Using these tools on an OCFS2 cluster node, you can extract your OCFS backup into the OCFS2 mountpoint.

## GFS - OCFS2 Comparison Table

| Feature | GFSv1 6.1 | OCFS2 1.2.3 |
|---|---|---|
| Release date | 2006-08 (v1.0 1996) | 2006-07 (v1.0 2005) |
| Linux kernel inclusion | out-of-tree | 2.6.16 |
| CPU architecture | x86, x64, ia64 | x86, x64, ia64, ppc, ppc64 |
| Max. supported nodes | 256 | 255 |
| Max. file name length | 255 | 255 |
| Max. path length | unlimited | unlimited |
| Block size | 512 B - 4 KB | 512 B - 4 KB |
| Cluster size | - | 4 KB - 1 MB |
| Max. file size | 2 TB / 16 TB / 8 EB | 4 TB / 16 TB / 4 PB |
| Max. fs size | 2 TB / 16 TB / 8 EB | 4 TB / 16 TB / 4 PB |
| Volume manager | LVM2 + CLVM | LVM2, EVMS |
| Lock manager | GULM, kernel DLM | OCFS2 DLM |
| Cluster manager | CMAN | O2CB (NM+HB+TCP) |
| Shared block devices | GNBD, FC, iSCSI | FC, iSCSI |
| Online/Offline resizing | grow/- | -/- |
| User/Group quotas | yes/yes | -/- |
| Multipath | yes | yes |
| Direct I/O | yes | yes |

# Exercise 10-1

## Set up an OCFS2

The purpose of this exercise is to familiarize you with OCFS2.

This exercise builds on the previous one, “Set up an iSCSI Target and an iSCSI initiator” on page 9-23.

You will find this exercise in the workbook.

*(End of Exercise)*

# Summary

| **Objective** | **Summary** |
| --- | --- |
| 1. | Global File System (GFS)<br>Under RHEL, primarily GFS (Global File System) is used as cluster file system. |
| 2. | Oracle Cluster File System 2 (OCFS2)<br>OCFS2 is the cluster file system used under SUSE Linux Enterprise Server 10.<br>The configuration is contained in `/etc/ocfs2/cluster.conf`; the program to create the file system is **mkfs.ocfs2**.<br>The clustering functionality is provided by the services **o2cb** and **ocfs2**. |

# SECTION A

## Appendix: AutoYaST

This section explains how to perform an automated installation using the AutoYaST feature of SUSE Linux Enterprise Server 10.

AutoYaST facilitates the roll-out of large numbers of machines. The installation is controlled by an XML file which contains the machine specific information, e.g. IP address, hostname, partitioning, etc. Manual intervention during the installation process is unnecessary.

The installation is started using a CD, a boot floppy disk or a PXE capable network card.

The installation source can be the set of CDs as well as an installation server in the network. The supported protocols for accessing the repository on the installation server are NFS, HTTP and FTP.

### Objectives

- Autoinstallation Basics
- Set up an Installation Server
- Create a Configuration File for AutoYaST
- Start the Installation

# Objective 1

## Autoinstallation Basics

Both Red Hat and SUSE Linux Enterprise Server 10 provide a way to automate installations:

- Kickstart on RHEL4
- AutoYaST on SUSE Linux Enterprise Server 10

### Kickstart on RHEL4

Red Hat uses the anaconda tool for the installation. If you set up the installation automatically this is referred to as kickstart environment.

The kickstart configuration file is a regular text file that contains the answers to installation questions in separate lines.

When installing a Red Hat system, a kickstart configuration file anaconda-ks.cfg will be created in the home directory of the root user (/root). This file contains the settings you entered during the installation. Before using it you have to uncomment the lines containing the partition setup.

To create a kickstart file from scratch you would use the tool system-config-kickstart. Manual editing of the file is required if you want to set up software raid or LVM.

### AutoYaST on SUSE Linux Enterprise Server 10

AutoYaST is the tool for automated installations on SUSE Linux Enterprise Server 10. All information needed during installation, e.g. partitioning or software selection, is provided by a control file in XML format. No manual intervention is necessary during the installation process.

If you have to install several systems with the same setup you can save time by automating the installation. Depending on your requirements, you can ensure all systems are set up with the same configuration, or configure systems individually with specific control files.

You should not confuse auto installation with cloning or imaging. An automated installation is a regular installation where answers to questions asked during the installation are contained in the control file. The hardware detection is still done so that the same control file can be used on diverse hardware. Imaging or cloning require identical hardware of source and target of the image.

AutoYaST is optimally used in conjunction with an installation server also providing a TFTP and a DHCP server. The advantages are:

- To start the installation, you only have to insert a suitable boot disk.
- The computer receives all information necessary for the installation via the network.
- In conjunction with wake-on-lan and/or PXE boot-enabled network interface cards, not even a boot disk is required.
- Even the on-site attendance of an administrator is not necessary for the installation.

The installation server can be accessed via the protocols NFS, HTTP and FTP.

This results in a highly simplified installation of a large number of individually configured computers.

AutoYaST can also be used to copy additional files into the installed system, as well as scripts which are executed at the end of the installation.

It is also possible to create a control file at installation time. In the last menu of the installation process you can check the box **Clone This System**. This will create an autoinst.xml file in the home directory of the root user (/root). The creation of an AutoYaST control file using the YaST AutoYaST module is covered later in this section.

![](img/63e88022bf135307e3eac051ad238b5b_451_0.png)

In this section, we will not cover a fully automated installation. Instead, we will use the CD 1 as a boot medium and access the installation repository via NFS. The control file will be provided on a floppy disk.

# Objective 2

## Set up an Installation Server

AutoYaST requires a certain layout of directories and files on the installation server.

The layout is described in http://www.suse.com/~ug/AutoYaST_FAQ.html.

The purpose of the YaST module “Installation Server” is to create an installation repository that is suitable for automated installation using AutoYaST.

It copies the needed files to their proper location and creates certain links and files.

For setting up the installation server, start the YaST module “Installation Server”.

1. Select `yast2 > Miscellaneous > Installation Server`

![](img/63e88022bf135307e3eac051ad238b5b_452_0.png)

or enter

`yast2 instserver`
