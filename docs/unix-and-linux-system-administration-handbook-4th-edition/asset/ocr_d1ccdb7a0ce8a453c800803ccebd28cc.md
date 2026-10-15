The output looks like this:

```
solaris$ modinfo
Id Loadaddr Size Info Rev ModuleName
1 ff0e000 3ba0 1 1 specfs (filesystem for specfs)
2 ff086000 1340 - 1 swapgeneric (root/swap config)
3 ff028200 1a56 1 1 TS (time sharing sched class)
4 ff084000 49c - 1 TS_DPTBL (Timesharing dispatch)
5 ff095000 15248 2 1 ufs (filesystem for ufs)
6 ff0b8000 20e0 1 1 rootnex (sun4c root nexus)
7 ff084400 170 57 1 options (options driver)
8 ff08dc00 2f4 62 1 dma (Direct Memory Access)
9 ff08c000 968 59 1 sbus (SBus nexus driver)
...
```

On our Solaris system, the list continued for 80-odd lines. Many elements that are hardwired into the kernel on other versions of UNIX (such as UFS, the local file system) are loadable drivers in Solaris. This organization should make it much easier for third parties to write packages that integrate easily and seamlessly into the kernel, at least in theory.

As described in Linux kernel configuration earlier in this chapter, you can add a driver with the add_drv command. This command loads the driver into the kernel and makes the appropriate device links (all links are rebuilt each time the kernel boots). Once you add_drv a driver, it remains a part of the system until you actively remove it. You can unload drivers by hand with rem_drv.

Whenever you add a driver by running add_drv, it is a good idea to also run drvconfig. This command reconfigures the /devices directory and adds any files that are appropriate for the newly loaded driver.

Loadable modules that are not accessed through device files can be loaded and unloaded with modload and modunload.

# 13.8 LINUX UDEV FOR FUN AND PROFIT

![](bbox=[0.22, 0.9, 0.26, 0.96])

Device files have been a tricky problem for many years. When systems supported only a few types of devices, manual maintenance of device files was manageable.

As the number of available devices has grown, however, the /dev filesystem has become cluttered, often with files irrelevant to the current system. Red Hat Enterprise Linux version 3 included more than 18,000 device files, one for every possible device that could be attached to the system! The creation of static device files quickly became a crushing problem and an evolutionary dead end.