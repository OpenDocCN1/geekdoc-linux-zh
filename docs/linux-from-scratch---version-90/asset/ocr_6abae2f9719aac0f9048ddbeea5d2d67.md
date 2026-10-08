# 6.2. Preparing Virtual Kernel File Systems

Various file systems exported by the kernel are used to communicate to and from the kernel itself. These file systems are virtual in that no disk space is used for them. The content of the file systems resides in memory.

By creating directories onto which the file systems will be mounted:

```
mkdir -pv $LFS/{dev,proc,sys,run}
```

# 6.2.1. Creating Initial Device Nodes

When the kernel boots, it requires the presence of a few device nodes, in particular the console and null devices. The device nodes must be created on the hard disk so they are available before udev has been started, and additionally when Linux is started with init=/bin/bash. Create the devices by running the following commands:

```
mkkn -m 600 $LFS/dev/console c 5 1
mknod -m 666 $LFS/dev/null c 1 3
```

# 6.2.2. Mounting and /dev

The recommended method of populating /dev directory with devices is to mount a filesystem (such as tmpfs) on the /dev directory, and allows the devices to be created dynamically on that virtual filesystem as they are detected or observed. Device creation is generally during the boot process by Udev. Since this new system does not have Udev and has not been booted, it is necessary to mount and populate /dev manually. This is accomplished by binding mount the system's /dev directory. A bind mount is a type of mount that allows you to create a mirror of a device directory or mount point to some other location. Use the following command to achieve this:

```
mount -v --bind $LFS/dev
```

# 6.2.3. Mounting Virtual Kernel File Systems

Now mount the remaining kernel filesystems:

```
mount -vt devpts devpts $LFS/dev/pts -o gid=5,mode=620
mount -vt proc proc $LFS/proc
mount -vt sysfs sysfs $LFS/sys
mount -vt tmpfs tmpfs $LFS/run
```

The meaning of the mount options for devpts:

```
gid=5
```

This ensures that all devpts-created device nodes are owned by group ID 5. This is the ID we will use later on the tty group. We use the group instead of a name, since the host system might use a different ID for its tty group.

```
mode=0620
```

This ensures that all devpts-created device nodes have mode 0620 (user readable and, group writable). Together with the option, this ensures that devpts will create device nodes that meet the requirements of grantpt(), meaning the Glibc pt_chown helper binary (which is not installed by default) is not necessary.