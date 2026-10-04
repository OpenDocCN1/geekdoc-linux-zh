```
Enter name of device instance number file [/etc/path_to_inst]:
root filesystem type [ufs]
Enter physical name of root device [/sbus@1,f8000000/esp@0,800000/sd@0,0:a]:
Configuring network interfaces: le0
Hostname: sol
(fsck messages)
The system is coming up. Please wait
(More messages)
sol login:
```

Boot information is displayed on the system console as the system boots. If you are not at the system console to watch the boot information, you can use the UNIX dmesg command to redisplay information that was displayed during the boot process or view the information in the /var/adm/messages file.

To view messages displayed during the boot process, use one of the following methods:

+   - At a UNIX prompt, type /usr/sbin/dmesg and press Enter. The boot messages are displayed.
- At a UNIX prompt, type more /var/adm/messages and press Enter.

# System Run States

After the kernel is initiated by the boot command, it begins several phases of the startup process. The first task is for OpenBoot to load the kernel. By default, the kernel is named /kernel/unix and is located in the /root partition on the disk, with its path defined in an OpenBoot PROM alias named disk. The kernel consists of a small static core and many dynamically loadable kernel modules. Many kernel modules are loaded automatically at boot time, but for efficiency, others—such as device drivers—are loaded in from the disk as needed by the kernel. When the kernel loads, the system reads a file named /etc/system. Parameters in this file modify how the kernel gets loaded. Occasionally, kernel parameters in this file need to be adjusted.

**CAUTION!** Do not modify the /etc/system file unless you are certain of the results. A good practice is always to make a backup copy of any system file you modify in case the original needs to be restored. Incorrect entries could prevent your system from booting.

After control of the system gets passed to the kernel, the system begins initialization and enters one of eight run states—also called init states—described in Table 1-6. The init state in which the system is running defines the services and resources available to users. When preparing to do a system administration task, you need to determine which init state is appropriate for the task. Use Table 1-7 in determining what init state to use for a particular task. A system can run in only one init state at a time.