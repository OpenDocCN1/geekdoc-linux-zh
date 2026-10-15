
Kickstart uses graphical mode by default, which defeats the goal of unattended installation. The text keyword at the top of the example fixes this.

The rootpw option sets the new machine's root password. The default is to specify the password in cleartext, which presents a serious security problem. You should always use the --iscrypted flag to specify a pre-encrypted password. Password entries from an /etc/shadow file work fine for an encrypted password, or you can try the /sbin/grub-md5-crypt tool on an already built system.

The clearpart and part directives specify a list of disk partitions with sizes. You can use the --grow option to ask one of the partitions to expand to fill any remaining space on the disk. This feature makes it easy to accommodate systems that have different sizes of hard disk. Advanced partitioning options, such as the use of LVM, are supported by Kickstart but not by the system-config-kickstart tool. Refer to Red Hat's on-line documentation for full disk layout options.

The second section is a list of packages to install, beginning with a %packages directive. The list can contain individual packages, collections such as @ GNOME, or the notation @ Everything to include the whole shebang. When selecting individual packages, specify only the package name, not the version or the .rpm extension. Here's an example:

```
%packages
@ Networked Workstation
@ X Window System
@ GNOME
mylocalpackage
```

In the third section of the Kickstart configuration file, you can specify arbitrary shell commands for Kickstart to execute. There are two possible sets of commands: one introduced with %pre that runs before installation, and one introduced with %post that runs afterward. Both sections have some restrictions on the ability of the system to resolve hostnames, so it's safest to use IP addresses if you want to access the network. In addition, the postinstall commands are run in a chrooted environment, so they cannot access the installation media.

## Building a Kickstart server

Kickstart expects its installation files to be laid out as they are on the distribution CD, with packages stored in a directory called RedHat/RPMS on the server. You can easily add your own packages to this directory. There are, however, a couple of issues to be aware of. If you don't want to install all packages, either list your supplemental packages individually in the %packages section of the ks.cfg file or add your packages to one or more of the collection lists. Collection lists are specified by entries such as @ GNOME and stand for a predefined set of packages whose members are enumerated in the file RedHat/base/comps on the server. Unfortunately, the comps file format is not well documented. The collections are the lines that begin with 0 or 1; the number specifies whether the collection is selected by default. In general, it's not a good idea to tamper with the standard collections. We suggest that you leave them as Red Hat defined them and explicitly name all your supplemental packages in the ks.cfg file.

## Pointing Kickstart at your config file

Once you've created a config file, you have a couple of ways to get Kickstart to use it. The officially sanctioned method is to boot with a DVD and ask for a Kickstart installation by specifying linux ks at the initial boot: prompt. If you don't specify additional arguments, the system determines its network address by using DHCP. It then obtains the DHCP boot server and boot file options, attempts to mount the boot server with NFS, and uses the value of the boot file option as its Kickstart configuration file. If no boot file has been specified, the system looks for a file called /kickstart/host_ip_address-kickstart.

Alternatively, you can tell Kickstart to get its configuration file in some other way by providing a path as an argument to the ks option. There are several possibilities. The instruction

```
boot: linux ks=http://server/path
```

tells Kickstart to use HTTP to download the file instead of NFS. Using ks=floppy tells Kickstart to look for ks.cfg on a local floppy drive.

To eliminate the use of boot media entirely, you'll need to graduate to PXE. See page 363 for more information about that.

## Using AutoYaST: SUSE's automated installation tool

![](img/14d78e3cecac4581d37024baf1e94cca_415_0.png)

YaST2 is SUSE's all-in-one installation and configuration tool. It comes with a nice GUI and is fun to use when installing a single system. AutoYaST, its automated equivalent, is the most powerful automated installation software of all the distributions described in this book. You can download detailed documentation from suse.com/~ug/autoyast_doc.

SUSE splits the autoinstallation process into three phases: preparation, installation, and configuration. Initial preparation is performed with the YaST2 AutoYaST module:

```
suse$ /sbin/yast2 autoyast
```

This module helps you define the details of your desired setup. The result of running it is an XML control file that tells the installer how to configure a SUSE
