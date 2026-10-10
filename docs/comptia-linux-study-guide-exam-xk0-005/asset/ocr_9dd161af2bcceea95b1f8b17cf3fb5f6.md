# **Listing 24.1**: Looking up disk information via the **`dmesg`** command

```
# dmesg | grep sde
[..]
[     5.566479] sd 6:0:0:0: [sde] Attached SCSI disk
```

The `dmesg` utility’s output is searched using `grep` to find information concerning the `sde` disk (`/dev/sde`). The important clue here is that the disk is an attached SCSI disk.

The available SCSI disk driver information is stored within a `/sys/` directory, as shown in Listing 24.2.

# **Listing 24.2**: Determining the driver via the `ls` and `udevadm` commands

```
# ls /sys/bus/scsi/drivers
sd    sr
#
# udevadm info -an /dev/sde | grep DRIVERS | grep sd
        DRIVERS=="sd"
```

Notice that the `sd` and `sr` drivers are used for SCSI devices. The `udevadm` command confirms which one is employed for the `/dev/sde` disk.

After the driver (module) is determined, use the `lsmod` command to see if it is currently loaded into the kernel. A snipped example is shown in Listing 24.3.

# **Listing 24.3**: Determining if the module is loaded using the `lsmod` command

```
# lsmod | grep sd
sd_mod                     4632  5
[..]
# modinfo sd_mod
filename:        /lib/modules/3.10.0-862.11.6.el7.x86_64/kernel/drivers/scsi/sd_mod.ko.xz
[..]
description:     SCSI disk (sd) driver
[..]
```

If the module is not loaded, it may be built into the kernel. You can check this by looking at the `modules.builtin` file, as shown snipped in Listing 24.4.

# **Listing 24.4**: Determining if the module is built in using the `cat` command

```
$ cat /lib/modules/$(uname -r)/modules.builtin | grep sd_mod
kernel/drivers/scsi/sd_mod.ko
```

If the module is not loaded or built into the kernel, dynamically load it using super user privileges and the `modprobe` command (Chapter 14, “Tending Kernel Modules”).