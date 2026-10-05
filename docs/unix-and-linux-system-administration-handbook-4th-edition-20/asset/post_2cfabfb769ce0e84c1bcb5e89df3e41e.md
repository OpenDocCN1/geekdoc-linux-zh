
# Chapter 12 Software Installation and Management

Kickstart uses graphical mode by default, which defeats the goal of unattended installation. The text keyword at the top of the example fixes this.

The rootpw option sets the machine's root password. The default is to specify the password in cleartext, which presents a serious security problem. You should always use the `--encrypted` flag to specify a pre-encrypted password. Password entries from an `--shadow/md5-crypt` file work for the encrypted password, or you use the `/sbin/grub-md5-crypt` tool on an already built system.

The clearpart and part directives specify a list of partitions with sizes. You can use the `--grow` option to ask one of the partitions to fill any remaining space on the disk. This feature makes it easy to accommodate systems that have different sizes of hard disk. Advanced partitioning options, such as the use of LVM, are supported by Kickstart but not by the `system-config-kickstart` tool. Refer to Red Hat's on-line documentation for disk layout options.

The second section is a list of packages to install, beginning with a `%packages` directive. The list can contain individual packages, collections such as @ GNOME, or the notation @ Everything to include the whole shebang. When selecting individual packages, specify only the package name, not the version or the .rpm extension. Here is an example:

```
%packages
@ Networked Workstation
@ X Window System
@ GNOME
mylocalpackage
```

In the third section of the Kickstart configuration file, you can specify arbitrary shell commands for Kickstart to execute. There are two possible sets of commands: one introduced with `%pre` before installation, and one introduced with `%post` after runs. Both sections have some restrictions on the ability of the system to resolve hostnames, so it's safest to use IP addresses if you want to access the network. In addition, the postinstall commands run in a rooted environment, so they cannot access the installation media.

# Building a Kickstart server

Kickstart executes its installation files to be laid out as they are on the distribution CD, with packages stored in a directory called RedHat/RPMS on the server. You can easily add your own packages to this directory. There are, however, a couple of issues to be aware of.

First, if you tell Kickstart to install all packages (with an @ Everything in the packages section of your ks.cfg), it installs the add-on packages in alphabetical order after the base packages have been laid down. If your package depends on other packages that are not in the base set, you may want to call your package something like zymackack.rpm to make sure that it gets installed last.

# Using YaAST: SUSE’s automated installation tool

If you don't want to install all packages, either list your supplemental packages individually in the %packages section of the ks.cfg file or add your packages to one or more of the collection lists. Collection lists are specified by entries such as GNOME and stand for a predefined set of packages whose members are enumerated in the RedHat/base/comps on the server. Unfortunately the comps file format is not well documented. The collections are the lines with 0 or 1; the number specifies whether the collection is selected by default. In general, it’s not a good idea to tamper with the standard collections. We suggest that you leave them as Red Hat defined and explicitly name all your supplemental packages in the ks.cfg file.

### Pointing Kickstart at your config file
Once you’ve created a config file, you have a couple of ways to get Kickstart to use it. officially sanctioned method is to boot with a DVD and for a Kickstart installation by specifying linux ks at the initial boot: prompt. If the system determines its network address by DHCP it obtains the DHCP boot server and boot file options, attempts to mount the boot server with NFS, and uses the value of the boot file option as its Kickstart configuration file. If no boot file has been specified, the system looks for a file called kickstart/host_ip_address-kickstart.

Alternatively, you can tell Kickstart to get its configuration file in some other way by providing a path as an argument to the ks option. There are several possibilities: the instruction

```
boot linux ks=http:server/path
```

ells Kickstart to use HTTP to download the file instead of NFS. Using=floppy tells Kickstart to look for ks.cfg on a local floppy drive.

To eliminate the boot media entirely, you’ll need to graduate to PXE. See page 363 for more information about that.

# Using YaAST: SUSE’s automated installation tool

YaST2 is SUSE’s all-in-one installation and configuration tool. It comes with a nice GUI and is fun to use when installing a single system. Auto YaAST, its automated version, is the most powerful automated installation software of all the distributions described in this book. You can download detailed documentation from suse.com/~ug/autoyast_doc.

SUSE splits the autoininstallation process into three phases: preparation, installation, and configuration. Initial preparation is performed with the YaST2 AutoYaST module:

```
suse$ /bin/yast2 autoyast
```

This module defines the details of your desired setup. The result of running it is an XML control file that tells the installer how to configure a SUSE

![](img/579efec8c67772f31ecf34844bbb71a2_415_0.png)

# Chapter 12 Software Installation and Management

system. The structure of the file is described in the on-line documentation mentioned above.

A couple of shortcuts can speed the configuration process. The AutoYaST module can read Kickstart configuration files to help you upgrade from "legacy" systems. If you want to duplicate the configuration of the machine you are currently on, an option activates this as well.

To perform an actual installation, you need three network services:

- DHCP server on the same subnet as the machine you want to set up
- SUSE installation server or package repository
- A server that provides the configuration information

The last of these setups can supply the configuration files through your choice of HTTP, NFS, or TFTP.

In the basic setup, you produce a control file for each machine you want to install. AutoYaST uses the IP address of the client to determine which control file to use. This approach is not especially efficient if you have to install a series of different machines.

You can create more complex setups using a rules system. Different control files are matched to the target system based on properties such as disk size, host ID, or PCMCIA availability. The contents of all selected control files are merged, with the last control file overriding earlier ones in the case of conflicts. (A control file does not have to specify all aspects of a system's configuration, so merging does make sense.)

Control files can also define "classes" of machines based on hostnames or IP address ranges, and each class may have another subsidiary control file associated with it. Machines can belong to zero, one, or multiple classes, and their configurations will incorporate the contents of all the appropriate class files.

Thanks to its ability to integrate the contents of multiple control files, the AutoYaST structure allows complex setups to be defined with minimal redundancy. The XML control files are somewhat cumbersome for humans to read, but the files are simple to process and edit with any of the commonly available XML tools.

# Automating installation with the Ubuntu installer

Ubuntu relies on the underlying Debian installer (named, appropriately enough, debian-installer) for "preseeding", the recommended method for automated installation. In Kickstart, a preconfiguration file answers questions asked by the installer. Preseeded installations cannot use existing partitions; they must either use free space or partition the entire disk.

All the interactive parts of the Debian installer use the debconf utility to decide which questions to ask and what default answers to use. By providing debconf
