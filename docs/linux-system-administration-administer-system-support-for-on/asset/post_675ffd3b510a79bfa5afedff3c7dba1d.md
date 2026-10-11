
7 194.ATM10-0-0.GW1.JAX1.ALTER.NET (146.188.232.173) 79.928 ms 81.824 ms 80.858 ms
8 bs-jackson-gw.customer.alter.net (157.130.65.226) 81.009 ms 80.869 ms 80.300 ms
9 host-205-152-78-160.jax.bellsouth.net (205.152.78.160) 82.432 ms 81.343 ms 81.254 ms
10 172.17.123.22 (172.17.123.22) 87.912 ms 87.148 ms 86.425 ms
11 netflow-cis-fe60-b252.nerdc.ufl.edu (128.227.252.153) 87.027 ms 88.596 ms 88.445 ms
12 cse-rsm.core.ufl.edu (128.227.254.131) 88.447 ms 94.889 ms 88.006 ms
13 grove.ufl.edu (128.227.8.9) 87.972 ms 87.721 ms 87.796 ms

Thirteen hops are required to get an IP packet (network information such as a telnet connection or e-mail) from shell13.ba.best.com to grove.ufl.edu. The packet goes through 13 networks in a matter of seconds, which is pretty good for a cross-country trip.

If either host is handling a lot of other network traffic, however, the connection may slow. The effect on performance is the same, whether over the Internet or on a smaller scale. If two hosts aren’t on the same network and have to connect to each other from relatively far apart, they could cause a bottleneck. If you’re going to network your Linux hosts, take their physical separation into account when you plan for your system usage.

![](img/8ad518fddafc7f5e73715a2604b61d50_86_0.png)

> The traceroute command is sometimes used as a tool to help an intruder find out how to reach your system from the Internet. You may want to make sure that other hosts in your control on that trip are secure.

## Understanding Networking

You’re not done yet. (System administrators have to get used to that phrase.) You’ve found out what your users’ needs are, you’re secured, and you’re backing up everything regularly—but you still need a networking strategy. Consider the following options:

- Connect to a corporate network
- Connect to an ISP
- Connect via PPP or ISDN

If you're connecting to anyone's network, be sure your host is extremely secure. When you connect to a corporate network, you'll have to follow the rules of the company and their Acceptable Use Policy. That means that any games you have on your system you may want to remove. Also note that other systems around you may not be secure; therefore, they should not be trusted.

When you connect to an ISP, whether via PPP or directly, remember that you're trusting their network security on their routers, hosts, and other network devices. This means taking note of who else is out there. You'll also be exposed to the Internet. Keep in mind that even as cool as Internet access is, it does have its share of problems. People will play around and try to get into your system because it's cool, not necessarily because of the information it has. The beauty of Linux is also its risk – its source code availability. Linux is the most robust Unix implementation due to the contributions of so many different people and the desire for a powerful, freely available operating system. Because the core code of all Linux operation is available to anyone, programmers or hackers can easily develop ways to exploit networking or system software. Although critics of Linux may say that's reason enough not to put it on the Web, they forget that for every system exploitation there's a fix, and the open source of Linux contributes just as much to the security-conscious as it does to those who would exploit it. Keeping yourself up to date on security advisories will help you plug holes before they fall into the hands of the clever teenagers who would break into your system.

![](img/8ad518fddafc7f5e73715a2604b61d50_87_0.png)

Chapter 11 covers networking basics in depth.

## Summary

A system administrator needs to keep the system running with minimal downtime. To do so, take these fundamental steps: keep good records and logs, listen to users, keep the system secure, and maintain your hardware.

Establish system security to prevent break-ins. You can plug quite a few holes by turning off unnecessary services and running data-integrity programs like Tripwire. It's also imperative to back up regularly and to have a cleanup plan in case your system is attacked. Make sure you understand your backup procedures and exactly how to restore your data. Also, keep an open line of communication with your users, maintaining (and reviewing as necessary) accessibility to the files.

If you're working in a growing computing environment, have an understanding and good planning for application scaling, setting up application servers, and working with network architecture. All these can have an impact on your day-to-day tasks, as well as on your system’s performance.

Healthy networks require administrators to keep good plans and records. You’ll need to know not only what type of connection you need, but also the impact it will have on your security. Remember: When you connect to a network, you’re trusting other systems and the data they provide. Trust, yes, but wisely.

# Chapter 3

# File System and Disk Management

IN THIS CHAPTER

- Understanding file-system structure
- Evaluating disk usage
- Creating swap space

THIS CHAPTER COVERS *disk partitioning*, the process of dividing your disk into smaller sections so it’s more manageable. It also examines swap space–what it is, what it does, and how to configure it.

## File-System Structure

In Linux, everything is a process or a file. In this section, I’ll talk about the importance of files to Linux and some ways to tweak them.

Linux sees your mouse as a file called `/dev/mouse`, your directory as a type of file, and your kernel as a file called `vmlinuz` or `bzImage`. Even your terminal is considered a file (`/dev/tty2` for example). If you’re going to run this operating system smoothly, first consider the file and how it’s structured – from the viewpoint of the operating system itself.

## Inode

The most vital part of a file is the *inode* – a data structure containing all the information that describes the file: size, permissions, location on disk, owners, groups, file type, and checksum. The inode is like a miniature database for a particular file. Listing 3-1 shows that the inode data structure for the Second Extended Filesystem, `ext2fs`, contains data, ownership, groups, file lists, directory access control lists, access and creation times, blocks, and the location of `ext2fs` on the disk.

### Listing 3-1: Using the /usr/src/linux/include/linux/ext2_fs_i.h file

```c
/*
 * linux/include/linux/ext2_fs_i.h
 *
 * Copyright (C) 1992, 1993, 1994, 1995
 * Remy Card (card@masi.ibp.fr)
 * Laboratoire MASI - Institut Blaise Pascal
 * Universite Pierre et Marie Curie (Paris VI)
 *
 * from
 *
 * linux/include/linux/minix_fs_i.h
 *
 * Copyright (C) 1991, 1992 Linus Torvalds
 */

#ifndef _LINUX_EXT2_FS_I
#define _LINUX_EXT2_FS_I

/*
 * second extended file system inode data in memory
 */
struct ext2_inode_info {
__u32 i_data[15];
__u32 i_flags;
__u32 i_faddr;
__u8  i_frag_no;
__u8  i_frag_size;
__u16 i_osync;
__u32 i_file_acl;
__u32 i_dir_acl;
__u32 i_dtime;
__u32 i_version;
__u32 i_block_group;
__u32 i_next_alloc_block;
__u32 i_next_alloc_goal;
__u32 i_prealloc_block;
__u32 i_prealloc_count;
int i_new_inode; /* Is a freshly allocated inode */
};
#endif /* _LINUX_EXT2_FS_I */
```

In Slackware Linux, the default size of an inode is 4096 bytes. You can change the size of the inode to 2048 or 1024 bytes, depending on the size of your disk partition (or if you plan to use a large number of small files). The advantage of larger inodes is that they require less disk I/O and offer better performance. As with any large file, however, an oversize inode can eat too much disk space. Smaller inodes offer exactly the opposite advantage (and problem): you can save kilobytes of disk space but your disk I/O increases (because there are more inodes to access) and your performance isn't as good.

If you want to see the inode, or index number assigned to a particular file or directory, type `ls -i` or `ls -inode`. The following list is an example of what you'll see:

```bash
$ ls -li
total 6
93475 -rw-r--r-- 1 stripes users    52 Aug 6 17:06 diskstuff
93474 -rw-r--r-- 1 stripes users  2935 Aug 6 17:07 inodes
95505 drwxr-xr-x 2 stripes users  1024 Aug 6 17:06 moreinfo
99569 drwxr-xr-x 2 stripes users  1024 Aug 6 17:07 morstuff
```

## The ext2fs commands

The Linux kernel for some time now has been using **ext2fs** for its preferred file system. Earlier file system types included **xiafs** and **extfs** (Extended File system). **The ext2fs** enables the most flexibility and is the only file system in which the kernel will run and compile. Let's go over the specific commands of **ext2fs**.

Suppose you've got a brand new hard drive you want to format for Linux. If you want to create a file system on it, the first step is to partition your disk. Then you can use mke2fs as follows:

```bash
# mke2fs /dev/hdb1
```

If you want to check for bad blocks first, use the -c option.

```bash
# mke2fs -c /dev/hdb1
```

At this point, you can also define the byte size of the inodes (as in the setup program).

```bash
# mke2fs -i 1024 /dev/hdb2
```

> **NOTE** Although the default inode size is 4096 bytes, you must define it as no smaller than 1KB (1024 bytes).

Fragments are not currently supported; don't use the -f option.
