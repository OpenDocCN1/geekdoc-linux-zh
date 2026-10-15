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

# Building a Kickstart server

Kickstart expects its installation files to be laid out as they are on the distribution CD, with packages stored in a directory called RedHat/RPMS on the server. You can easily add your own packages to this directory. There are, however, a couple of issues to be aware of.