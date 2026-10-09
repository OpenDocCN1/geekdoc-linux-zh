The system console is defined and activated in the next step with the `cfgcon` command. There are four possible LED display values associated with the console definition. If the console is not configured or there are multiple `try` definitions, then c31 is displayed and a menu is displayed for you to define the console. If the console is found to be a low-function terminal, iff (graphic), the LED display will read c32. If the console is found to be a tty, Lflf will display c33, and if the console is a file, then c34 is displayed.

If your system is set to use the Common Desktop Environment (CDE), then CDE is started and you will see a graphical boot. You can also configure CDE so that the boot process is not graphical, but the operation mode is graphical. This is the way I always configure a machine running CDE. I run CDE this way because I have had machines act strangely and for various reasons the graphical boot did not start. To get around this, I just configure CDE to start only at the login prompt and with an ANSI2 boot.

The final step is synchronizing the ODM in the BLV with the ODM in the root filesystem, /etc/objrepos. The `savebase` command accomplishes this task.

We still have a few more steps. The `syncd` daemon is started, and all of the data in memory is written to disk. Next the `ermdemon` daemon is started. This is the process that writes to the system error log. After this, you will not see any more LED display, unless the system crashes, and then you see flashing 888!

The `/etc/no/login` file is removed from the system, if it exists. This is a nice tool to lock out all nonroot users from the system. If you forget to remove the `/etc/nologin` file, it will be removed for you. However, you may want to keep users locked out if you are doing maintenance, so remember to create another one after the reboot. If the hardware configuration has changed or is out of sync with the ODM, then you will see a message during the boot to run `diag -a`. You can run this on a live and active system, since it is just cleaning up the ODM.

The final message on the console is System Initialization Complete. At this point, `rc.boot 3` ends execution, and the rest of the `/etc/inittab` file is processed.

# FAST BOOT ON MP MACHINES WITH MPFCG COMMAND OPTION

Booting a multiprocessor machine with a large amount of memory and a bunch of devices can take a very long time. I have a pair of J-50s with about 350 SSA disks in an HACMP cluster. It takes 45 minutes to do a fast boot, and that is not even counting the time it takes to start the HACMP-controlled applications. That time is doubled if the fast boot is not set. IBM knows about this and has supplied the `mpfcg` command. (The `mpcfg` command works only with multiprocessor machines that have Mivro Channel I/O.) To always have a multiprocessor system fast boot (in relative terms), add the following command to the `/etc/inittab` file:

```
fastboot:2:once:/usr/sbin/mpfcg -cf 11 1 1 >/dev/console2>&1 # Fast boot
```