# Using SELinux 545

Some programs may have trouble working correctly when exec-shield is enabled. If you have to turn off exec-shield, log in as root and type the following command from a terminal window:

```
echo 0 > /proc/sys/kernel/exec-shield
```

That command sets the exec-shield kernel option to 0. The exec-shield option can take one of three values — 0, 1, and 2. Think of these values as three different levels of security. Table 2-2 summarizes the meaning of the three values of exec-shield. Fedora Core sets exec-shield to 1 by default.

| This Value of exec-shield | Has This Meaning |
| :--- | :--- |
| 0 | exec-shield is always disabled. |
| 1 | exec-shield is enabled for programs compiled with the newest version of gcc compiler. |
| 2 | exec-shield is always enabled. |

![](bbox=[0.137, 0.443, 0.203, 0.513])

To set exec-shield to its default value, type:
echo 1 > /proc/sys/kernel/exec-shield

# Using SElinux

Fedora Core comes with Security Enhanced Linux (SELinux), which provides mandatory access control with a much finer-grained control than just user and group ownership of files and processes. The access control is determined by the SELlinux policy that specifies the access permissions for everything — files, devices, programs, and users — in the system. Fedora Core comes with a default security policy that works out of the box. If you install Fedora with SELinux (by typing sellinux at the boot: prompt), you don't have to do anything and users or processes can access various system resources, such as files and devices.

For the fine-grained access control, SELinux requires a security context — think of it as the security attributes of the file or directory. Adding contexts to the files is referred to as labeling the filesystem. The filesystem is already labeled when you install Fedora Core and enable SELinux. However, if you need to re-label a filesystem, you can do so with the setfiles or fixfiles command.

Book VII
Chapter 2

Securing the Host