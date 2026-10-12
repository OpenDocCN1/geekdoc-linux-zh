/sbin/lilo, the map installer. Naturally, you can also do this manually after your system is installed, by editing the lilo.conf file and running /sbin/lilo at the command prompt.

> **Note**
> 
> Learning how to manipulate the lilo.conf file and use the map installer, /sbin/lilo, is highly recommended. There are a plethora of configuration options that you can choose from with LILO. The Red Hat installation program constructs only the most basic configuration file. Some of the more interesting options available are described later in this chapter in the section “LILO Tips and Tricks.”

The following listing shows the lilo.conf file needed to install LILO on the Linux root partition.

```
#
# General section
#
boot = /dev/hda1
install = /boot/boot.b
verbose = 2
prompt

# After 5 seconds, boot the default image
timeout = 50

#
# Boot my Linux 2.2.5 kernel
#

image = /boot/vmlinuz-2.2.5
    label = linux
    root = /dev/hda1
    read-only
    initrd = /boot/initrd.gz
```

The primary line of interest in the preceding file is boot = /dev/hda1. This line tells LILO where to install itself. By changing this line as shown in the following file listing, LILO will instead load itself into the master boot record.

```
#
# General section
#
```