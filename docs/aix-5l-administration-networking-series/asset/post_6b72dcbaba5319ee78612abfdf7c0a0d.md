
is still using the BLV loaded in RAM. In the next step, the kernel starts the **init** process (PID = 1), which is retrieved from the BLV. At this point, the **init** process takes over control of the boot process.

## Steps to get to Kernel Control

- Retrieve boot device list from NVRAM.
- Locate boot device from list.
- Load and validate boot record.
- Load boot image into reserved RAM.
- Pass control to boot kernel.

## Boot Sequence for the init Process

The **init** process is now in control of the boot process. The **init** process executes three phases of the boot process by invoking the **rc.boot** command with **1**, **2**, and **3** as command arguments. Each of these three phases takes on certain responsibilities. The first phase initializes the hardware to get the system booted. The second phase mounts the file systems as a RAMFS, or RAM filesystem. The third phase completes the hardware configurations and starts the init process, and then the /etc/inittab file is read and processed.

## Phase 1 of rc.boot

The first **rc.boot** phase is with the command **rc.boot 1**. This first phase initializes only the devices required to get the system booted, but not all devices are configured during the first phase. The **restbase** command is executed and copies the ODM in the BLV to the RAM filesystem. If **restbase** completes without error, the LED display will show 510. If the **restbase** command fails, the LED display will show 548. In the next step, the Configuration Manager (**cfmgr**) is run for phase 1, **cfmgr -f**. The **cfmgr** command queries the ODM for the objects in the Only\_Rules class and executes anything under the Phase 1 stanza. This step configures only the devices needed to get the system booted.

## Phase 2 of rc.boot

The **init** process next starts **rc.boot** phase 2 by executing **rc.boot 2**. During this boot phase, the LED display will show 551. In this second phase, the root volume group (rootvg) is varied online with the **ipl\_varyon** command. If the **ipl\_varyon** command completes successfully, the LED display will show 517. If the **ipl\_varyon** command fails, then the LED code will show 552, 554, or 556 and the system stops. If the **ipl\_varyon** command succeeds, then a filesystem check (**fsck**) is performed on the root filesystem, which is the **hd4** logical volume. If the **fsck** fails, the LED display will show 555. After a successful filesystem check, the /dev/hd4 logical volume is mounted on the RAM root filesystem. If the mount fails, the LED display will show 557 and the system stops. This LED code usually indicates a corrupted JFS log.

Next, in order, filesystem checks and mounting is done on **hd2** (/usr), **hd9var** (/var) and paging (**hd6**). If the **hd2** mount fails, the LED display will show 518, the boot process ends, and the system stops. When the /var filesystem is mounted, the **copycore** command checks the system to see if there has been a system dump since the last reboot. If a system dump is found, the **copycore** command copies the dump from **hd6** (paging space) to `/var/adm/ras`. If there is not enough filesystem space, you will be prompted to copy the dump to a tape device. However, the system can be **configured** so that this will not stop the boot process to prompt for the dump tape (see **sysdumpdev** command). At this point the paging space, **hd6**, is ready for mounting.

In the **rc.boot** phase 1, **rc.boot 1**, all of the base devices needed to get the system started are configured in the ODM of the RAM filesystem. We need to copy these device configurations to disk. The `cp /tmp/mnt/etc/objrepos` command copies the ODM data to disk. At this point, both copies of the ODM, **hd4** and **hd5**, are synced.

Up to now, there has not been a console available to view the boot progress, only LED display codes. All of the boot information has been written to a special boot log file. To view the system boot log, you must use the **alog** command.

```
# alog -t boot -o
```

Using this command, you can view the entire boot process log.

All of this has been done in the RAM filesystem so far. In AIX 5L, the access to the RAM filesystem was changed. To access the RAM filesystems, the prefix /.../ is added, for example /.../usr to access the /usr mount point in the RAM filesystem.

The RAM filesystem is no longer needed, so the kernel replaces the **init** in the BLV with the **init** in / (the **hd4** logical volume is mounted as the root filesystem), then clears the RAMDISK from memory.

## Phase 3 of rc.boot

In this final step, the */etc/init* is started and **init** goes through the /etc/inittab file and executes each entry for the run level for which we are booting, the default is specified on the first line of the /etc/inittab file. The default run level in AIX is run level 2. The LED display will show 553 while the /etc/inittab file is being processed. While processing the /etc/inittab file, **rc.boot** is called for a third time (**rc.boot 3**).

In **rc.boot** phase 3, **fsck** is run on the /tmp filesystem and is mounted. Next the root volume group is synchronized using **syncvg rootvg**. In the final part of **rc.boot 3**, the **cfmgr** command is executed again and configures all of the remaining devices on the system that were skipped in **rc.boot** phase 1. For a normal boot, **cfmgr** runs with the **-p2** switch, for Configuration Manager phase 2. For a service boot, **cfmgr** command runs with the **-p3** switch for Configuration Manager phase 3. Depending on the command switch provided to the **cfmgr** command, the ODM is queried for the **Config_Rules** ODM class. For **cfmgr -p2**, the methods under the **phase2=2** stanza are executed. For **cfmgr -p3**, the methods under the **phase3=3** stanza are executed. After the methods are executed, all of the remaining system devices that were skipped in **rc.boot** phase 1 are configured.

The system console is defined and activated in the next step with the `cfgcon` command. There are four possible LED display values associated with the console definition. If the console is not configured or there are multiple `tty` definitions, then c31 is displayed and a menu is displayed for you to define the console. If the console is found to be a low-function terminal, iff (graphic), the LED display will read c32. If the console is found to be a tty, Lflf will display c33, and if the console is a file, then c34 is displayed.

If your system is set to use the Common Desktop Environment (CDE), then CDE is started and you will see a graphical boot. You can also configure CDE so that the boot process is not graphical, but the operation mode is graphical. This is the way I always configure a machine running CDE. I run CDE this way because I have had machines act strangely and for various reasons the graphical boot did not start. To get around this, I just configure CDE to start only at the login prompt and with an ANSI2 boot.

The final step is synchronizing the ODM in the BLV with the ODM in the root filesystem, /etc/objrepos. The `savebase` command accomplishes this task.

We still have a few more steps. The `syncd` daemon is started, and all of the data in memory is written to disk. Next the `errpt` daemon is started. This is the process that writes to the system error log. After this, you will not see any more LED display, unless the system crashes, and then you see flashing 888!

The `/etc/nologin` file is removed from the system, if it exists. This is a nice tool to lock out all non-root users from the system. If you forget to remove the `/etc/nologin` file, it will be removed for you. However, you may want to keep users locked out if you are doing maintenance, so remember to create another one after the reboot. If the hardware configuration has changed or is out of sync with the ODM, then you will see a message during the boot to run `diag -a`. You can run this on a live and active system, since it is just cleaning up the ODM.

The final message on the console is System Initialization Complete. At this point, `rc.boot 3` ends execution, and the rest of the `/etc/inittab` file is processed.

## FAST BOOT ON MP MACHINES WITH MPFCG COMMAND OPTION

Booting a multiprocessor machine with a large amount of memory and a bunch of devices can take a very long time. I have a pair of J-50s with about 350 SSA disks in an HACMP cluster. It takes 45 minutes to do a fast boot, and that is not even counting the time it takes to start the HACMP-controlled applications. That time is doubled if the fast boot is not set. IBM knows about this and has supplied the `mpfcg` command. (The `mpcfg` command works only with multiprocessor machines that have Micro Channel I/O.) To always have a multiprocessor system fast boot (in relative terms), add the following command to the `/etc/inittab` file:

```
fastboot:2:once:/usr/sbin/mpcfg -cf 11 1 1 >/dev/console2>&1 # Fast boot
```
