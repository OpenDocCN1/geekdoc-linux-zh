
# Chapter 28 ♦ Emulation and Virtualization 711

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_755_0.png)

**Figure 28-9:** Setting Xen disk image options in YaST

- 6. Click Next to proceed with the actual Xen Machine installation. YaST creates a root filesystem image and stores it in a subdirectory of /var/lib/xen/images with the same name as the virtual machine that you are creating. YaST also creates a template domain configuration file by the name and stores it in /etc/xen.

That's all there is to. You will still need to add information such as the name of the Xen kernel to the template domain configuration file created in /etc/xen, but YaST has done the hard part of creating a filesystem image for you. The next section explains how to manually customize a Xen domain configuration file.

## Creating Xen Virtual Machines Manually

While the YaST Virtual Machine Installation (Xen) module simplifies the task of creating Xen virtual machines, it is not completely customizable. You may want to migrate existing Xen virtual machines or install them in a way that no one could anticipate. For this reason, it is also useful to understand how to create and configure Xen virtual machines. The following sections discuss the various aspects of a Xen virtual machine and how to perform each step manually.

## Creating Xen Root Filesystems

As mentioned previously, each operating system instance running under Xen must have its own root filesystem. The root filesystem used by Xen domain 0 is typically the root filesystem on your Linux system. Root filesystems for other Xen domains can be easily created using YaST. You can create these in two ways — by installing Linux into a filesystem or by using the YaST Virtual Machine Configuration module and doing filesystem/creation as part of your virtual machine setup. This section explains the former approach.

The root filesystem used by an operating system under Xen can be any root filesystem supported by that operating system — a physical disk, an NFS-mounted root, a filesystem image contained in a file, and so on. These must be created in the standard format. When created, you can use the SUSE YaST administration suite to populate them from your SUSE installation.

> For convenience, many people create root filesystems and associated partitions within local volumes. This provides flexibility that enables you to significantly increase the size of these filesystems or modify their configuration as needed, without requiring that you add disks or modify existing, partitions.

To use YaST to install a bootable SUSE distribution into a specified root filesystem location, mount the partition, NFS location, or file as /var/tmp/dirinstall on your SUSE system, and then start YaST. Select Software and then install into Directory, which displays the screen shown in Figure 28-10.

This screen is analogous to the standard SUSE installation screen. You can change the packages installed into the new root filesystem by clicking Change or selecting the Software link. When you have made the modifications to the contents of the root filesystem for your new Xen domain, click Next to begin the installation process, which displays a standard installation screen (see Figure 28-11).

The standard SUSE installation process on a Linux system automatically creates user, group, and system configuration files in a target root filesystem during the installation process. Because the YaST Installation into Directory populates only the root filesystem for Xen, you must perform a few manual steps before the filesystem is actually ready to be used with Xen.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_757_0.png)

Figure 28-10: The YaST Installation into Directory option

After the installation has completed, you should do the following:

- 1. Add any loadable kernel modules required for the Linux kernel to the new filesystem. You can do this from the command line (as root user) with a command like the following, `xen-kernel-dir` is the name of the directory containing the loadable kernel modules associated with the Xen-enabled Linux that you will be booting on a virtual machine:

```bash
(cd /lib/modules/; tar -cf xen-kernel-dir) | \
(cd /var/tmp/install/lib/modules; tar - xf -)
```

- 2. Create appropriate `/etc/passwd`, `/etc/shadow`, and `/etc/group` files for the Xen domain in which you are creating. You can do this by copying files from your primary root filesystem into the `etc` subdirectory of the directory in which you are creating a root filesystem for Xen.

- 3. Create an appropriate `/etc/fstab` file for the Xen system on which you will use the root filesystem that you are creating. The entries in this `fstab` file will reflect the names of partitions as seen by the Xen domain that you are creating, which will differ from the names on the Linux system where the files or partitions are actually stored. See the later section in this section titled "Creating Xen Configuration Files" for information on how to specify the name by which your Xen domain will see the partitions or filesystem images.

- 4. Create appropriate startup/runlevel links. As discussed in the section "Creating Xen Configuration Files," the runlevel in your Xen domains can be defined in the configuration file. You typically use runlevel 4, which is a custom runlevel and also the default runlevel in the example configuration files provided with Xen. This enables you to customize the processes that are normally started in the SUSE runlevel.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_759_0.png)

Thread-local storage, is implemented in current versions of glibc and its associated threading package, can cause problems with applications running under Xen. Its implementation under Xen can also be very slow. To disable thread-local storage under Xen and thus fall back to the simpler mechanisms used by earlier versions of glibc, move the file /lib/tls to /lib/disabled in each filesystem that you use with a Xen domain. If you do not, you will receive a warning message in the console log for each Xen domain that you start other than 0.

## Creating Swap Space for Xen Domains

After you have created a root filesystem for a new Xen domain, you should also prepare a swap file or partition for that domain. Like any Linux system, any operating system running under Xen must also have a swap partition. This partition can be a file or disk partition, and formatted using the standard mkswap command.

Make sure that an entry for the swap partition exists in the /etc/fstab file in the root filesystem for your Xen domain. With the root filesystem, the entry for the swap partition in fstab will reflect the name of the swap partition as seen by the Xen domain, which will usually differ from its names on the Linux system where the files or partitions are actually stored. See the following section, "Creating Xen Configuration Files," for information on how to specify the name by which your Xen domain will see your swap partition.

## Creating Xen Configuration Files

Xen configuration files are typically stored in the /etc/xen directory and can have any name. The name of the Xen configuration used when starting a Xen domain other than dom 0 is specified by the xm command line, as explained in the following section.

The SU Xen implementation includes two sample configuration files that you can use as starting points for defining your own domains. The first, /etc/xen/xmexample1, is a template for a simple domain configuration file and is the one that we'll focus on this section. The second, /etc/xen/xmexample2, is a more complex domain configuration file that accepts command-line arguments and is suitable
