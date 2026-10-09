
## BusyBox init

Among the commands it supports by default, BusyBox provides `init`-like capabilities. BusyBox `init` is particularly well adapted to embedded systems because it provides most of the `init` functionality an embedded system typically needs without dragging the weight of the extra features found in System V `init`. Also, because BusyBox is a single package, there is no need to keep track of an additional software package when developing or maintaining your system. There are cases, however, where BusyBox `init` may not be sufficient, for example, it does not support multiple runlevels.

Since we already described how to obtain, configure, and build BusyBox, we will limit this discussion to the setup of the `init` configuration files.

Because `/sbin/init` is a symbolic link to `/bin/busybox`, BusyBox is the first application to run on the target system. BusyBox identifies that the command being invoked is `init` and immediately jumps to the `init` routine.

BusyBox’s `init` routine carries out the following main tasks in order. (Action types are defined in the `inittab` file, described later in this section.)

- 1. Sets up signal handlers for `init`.
- 2. Initializes the console. By default, it uses the device specified with the kernel’s `console` boot option. If no console was specified to the kernel, BusyBox tries to use `/dev/console`.
- 3. Parses the `inittab` file, `/etc/inittab`.
- 4. Runs the system initialization script. (`/etc/init.d/rcS` is the default for BusyBox.)
- 5. Runs all the `inittab` commands that block (action type: `wait`).
- 6. Runs all the `inittab` commands that run only once (action type: `once`).

After completing these steps, the `init` routine loops forever, carrying out the following tasks:

- 1. Runs all the `inittab` commands that have to be respawned (action type: `respawn`).
- 2. Runs all the `inittab` commands that have to be asked for first (action type: `askfirst`).
- 3. Waits for child processes to exit.

After having initialized the console, BusyBox checks for the existence of an `/etc/inittab` file. If no such file exists, BusyBox uses a default `inittab` configuration. Mainly, it sets up default actions for system reboot, system halt, and `init` restart. Also, it sets up actions to start shells on the console and on the virtual consoles from `/dev/tty2` to `/dev/tty4`, although it will skip consoles without complaining if you haven't created the virtual console device entries.

If an `/etc/inittab` file is found, it is parsed, and the commands it contains are recorded inside internal structures to be carried out at the appropriate time. The format of the `inittab` file as recognized by BusyBox is well explained in the documentation included in the BusyBox package, which also includes an elaborate example `inittab` file.

Each line in the `inittab` file follows this format:

`id:runlevel:action:process`

Although this format resembles that of traditional System V `init`, take note that the meaning of `id` is different in BusyBox `init`. Mainly, the `id` is used to specify the controlling tty for the process to be started. If you leave this entry empty, BusyBox `init` will use the system console, which is fine when the process to be started isn't an interactive shell, or when you start a shell on the console. BusyBox completely ignores the `runlevel` field, so you can leave it blank. The `process` field specifies the path of the program to run, along with its command-line options. The `action` field is one of eight recognized actions to be applied to `process`, as described in Table 6-6.

**Table 6-6. Types of `inittab` actions recognized by BusyBox `init`**

| Action | Effect |
| :--- | :--- |
| `sysinit` | Provides `init` with the path to the initialization script. |
| `respawn` | Restarts the process every time it terminates. |
| `askfirst` | Similar to `respawn`, but is mainly useful for reducing the number of terminal applications running on the system. It prompts `init` to display “Please press Enter to activate this console.” at the console and waits for the user to press Enter before starting the process. |
| `wait` | Tells `init` that it has to wait for the process to complete before continuing. |
| `once` | Runs the process only once without waiting for its completion. |
| `ctrlaltdel` | Runs the process when the Ctrl-Alt-Delete key combination is pressed. |
| `shutdown` | Runs the process before shutting the system down. |
| `restart` | Runs the process when `init` restarts. Usually, the process to be run here is `init` itself. |

The following is a simple `inittab` file for our control module:

```
::sysinit:/etc/init.d/rcS
::respawn:/sbin/getty 115200 ttyS0
::respawn:/control-module/bin/init
::restart:/sbin/init
::shutdown:/bin/umount -a -r
```

This `inittab` file does the following:

- 1. Sets `/etc/init.d/rcS` as the system initialization file.
- 2. Starts a login session on the serial port at 115200 bps.
- 3. Starts the control module's custom software initialization script.
- 4. Sets `/sbin/init` as the program to execute if `init` restarts.
- 5. Tells `init` to run the `umount` command to unmount all filesystems it can at system shutdown and set the others as read-only to preserve the filesystems.

However, none of these actions takes place until `init` runs the system initialization script. This script can be quite elaborate and can actually call other scripts. Use it to set all the basic settings and initialize the various components of the system that need special handling. Particularly, this is a good place to:

- Remount the root filesystem in read-write mode.
- Mount additional filesystems.
- Initialize and start networking interfaces.
- Start system daemons.

Here is the initialization script for the control module:

```
#!/bin/sh

# Remount the root filesystem in read-write (requires /etc/fstab)
mount -n -o remount,rw /

# Mount /proc filesystem
mount /proc

# Start the network interface
/sbin/ifconfig eth0 192.168.172.10
```

This initialization script depends on the existence of an `/etc/fstab` file in the target's root filesystem. We won't discuss the contents and use of this file, because it is already explained in many documentation sources, such as the `fstab` manpage and *Running Linux*. Nevertheless, here's the `/etc/fstab` file used for the development of my control module:

```
# /etc/fstab
# device      directory   type      options
#
/dev/nfs      /           nfs       defaults
none          /proc       proc      defaults
```

In this case, we mount the target's root filesystem on NFS to simplify development. Chapter 8 discusses filesystem types, and Chapter 9 discusses NFS mounts.

## Minit

Minit is part of the miniaturized tools developed by Felix von Leitner, such as diet libc and embutlis, and is available at `http://www.feje.de/minit/`. As with the other tools distributed by Felix, Minit requires a properly configured diet libc.

Minit's initialization procedure is a complete departure from the traditional System V *init*. Instead of using `/etc/inittab`, for instance, Minit relies on the existence of a properly built `/etc/minit` directory. Firdtof Busse provides a description of how Minit operates at `http://www.fhunet.de/minit.shtml`. He also provides pointers to example `/etc/minit` directories.

By default, Minit's *Makefile* installs Minit components in the host's root filesystem. You can use the `DESTDIR` *Makefile* variable to install Minit in another directory:

```
$ make DESTDIR=${PRJROOT}/rootfs install
```

> —Michael Opdenacker
