+   * The **init** process was presented in detail. This powerful system-configuration and control utility can serve as the basis for your own embedded Linux system. System initialization based on **init** was presented, along with example startup script configurations.
+   * Initial ramdisk is a Linux kernel feature to allow further startup behavior customization before mounting a final root file system and spawning **init**. We presented the mechanism and example configuration for using this powerful feature.
+   * **initramfs** simplifies the initial ramdisk mechanism, while providing similar early startup facilities. It is easier to use, does not require loading a separate image, and is built automatically during each kernel build.

# #### 6.7.1 Suggestions for Additional Reading

File System Hierarchy Standard
Maintained by freestandards.org
www.pathname.com/fhs/

Boot Process, Init and Shutdown
Linux Documentation Project
http://tldp.org/LDP/intro-linux/html/sect_04_02.html

Init man page
Linux Documentation Project
http://tldp.org/LDP/sag/html/init.html

A brief description of System V init
http://docs.kde.org/en/3.3/kdeadmin/ksysv/what-is-sysv-init.html

*Booting Linux: The History and the Future*
Werner Almesberger
www.almesberger.net/cv/papers/ols2k-9.ps