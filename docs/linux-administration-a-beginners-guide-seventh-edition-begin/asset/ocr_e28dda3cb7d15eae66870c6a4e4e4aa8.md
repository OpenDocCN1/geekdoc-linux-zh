# CHAPTER 10 Knobs and Dials: API (Virtual) File Systems

> NOTE You should, of course, first make sure that the /etc/sysctl.conf file does not already contain an entry for the key that you are trying to tune. If it does, you can manually edit the file and change the value of the key to the new value.

# Issues on High-Volume Servers

Like any operating system, Linux has finite resources. If the system begins to run short of resources while serving requests (such as web access requests), it will begin refusing new service. The /proc entry /proc/sys/fs/file-max specifies the maximum number of open files that Linux can support at any time. The default value on our system was 201766, but this may be quickly exhausted on a busy system with network connections. Raising it to a larger number, such as 301598, can be useful. Using the sysctl command, type the following:

```
[root@server ~]# sysctl -w fs.file-max=301598
fs.file-max = 301598
```

Don't forget to append your change to the /etc/sysctl.conf file (or to a property named under the /etc/sysctl.d/) if you want it to be persistent.

# Debugging Hardware Conflicts

Debugging hardware conflicts on older hardware is always a chore. You can easing the burden by using some of the entries in /proc. These two entries are specifically designed to tell you what's going on with your hardware:

+   - /proc/iports tells you the relationships of devices to I/O ports and whether any conflicts exist. With Peripheral Component Interconnect (PCI) devices becoming dominant, this isn't as big an issue. Nevertheless, on the off-chance you have to deal with a motherboard Industry Standard Architecture (ISA) slots, you'll always have the information in /proc/iports handy.

+   - /proc/interrupts shows you the association of interrupt numbers to hardware devices. Again, like /proc/iports, PCI is making this less of an issue.

# SysFS

SysFS (short for file system) is similar to the proc file system. The major similarities between the two are that they are virtual file systems (in-memory file systems) and that both provide a information (data structures, actually) to be exported from the kernel to the user space. SysFS is usually mounted at the /sys mount point. The SysFS system can be used to obtain information about kernel objects, such as devices, modules, the system bus, firmware, and on. This system provides a view of the device tree (among other things) as the kernel sees it. It displays most of the known attributes of detected devices, such as the device name,