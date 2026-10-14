Added modular
Boot image: /vmlinuz
Added linux
The boot sector and the map file have *NOT* been altered.

If everything is all right, then you can create the boot sector by issuing

```
[root@digital /boot]# lilo -v
LILO version 20, Copyright 1992-1997 Werner Almesberger
Reading boot sector from /dev/hda
Merging with /boot/boot.b
Mapping message file /boot/message
Boot image: /boot/vmlinuz-2.0.35-apm
Added vmlinuz-apm *
Boot image: /boot/vmlinuz-2.0.35-modular
Added modular
Boot image: /vmlinuz
Added linux
/boot/boot.0300 exists - no backup copy made.
Writing boot sector.
```

You are now ready to test your new kernel. Shut down and reboot the system to begin module configuration. If you have any problems, hit Tab when rebooting and type the label of your previous kernel.

# Configuring the New Modules and Rebooting

Once you have successfully booted into your new kernel, you might think you are finished, but this isn’t the case. The drivers you compiled as modules haven’t yet been made active. To make them active, you need to do a little bit of configuration.

The Caldera boot system looks for a directory in the /etc/modules directory named after the version of the kernel you built. (In my example the full path of this directory is /etc/modules/2.0.35.) In this directory it expects to find a file named after the time and date when the kernel was built followed by a .default:

```
#1 Tue Jan 6 16:44:51 MET 1998.default
```

This is a weird name for a file. The name the system expects is stored in the kernel itself. To access it, you can use the following command:

```
[alberto@digital 2.0.35]$ uname -v
#2 Sat Oct 3 13:17:24 CDT 1998
```

Using this text, you’ll create the new module list so that the system will load your modules each time it boots. The command you’ll use to do this is a little bit complicated, but with a look at the BASH man page you might be able to figure out that you’re using a technique called command substitution:

```
# find /lib/modules/2.0.35-apm -name "*.o" -print > " /etc/modules/2.0.35/ $(uname -v).default"
```

This command finds all the modules in the new modules directory, makes a list of them, and sends it to the correct file in the /etc/modules/2.0.35 directory. Without such a complex command, this is tedious work and no tool currently automates this process. If you don’t do this, your new modules won’t load automatically when the computer starts.

Once this has been done, shut down again and reboot using your new kernel. If everything goes as planned, your new modules will now be active. Welcome to your new system!