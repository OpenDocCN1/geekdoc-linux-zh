
- **Boot block 1 (boot1)**. This is a very simple program that runs from the boot sector of the slice you selected in boot0, and its job is to use a stripped-down version of disklabel (what divides a slice up into BSD-style partitions, which we will cover in the next hour) to find and run boot2 in the appropriate partition. There is no user-interface portion to boot1.
- **Boot block 2 (boot2)**. Finally, you reach a boot block that has enough elbow room to have the necessary complexity to read files on the bootable filesystem in its BSD partition. The job of boot2 is to run a program called loader, which gives you a user interface that allows you to control the way the kernel loads. We will get to the kernel shortly.
- **loader**. You can find this program in the /boot directory. It reads the /boot/defaults/loader.conf and /boot/loader.conf configuration files, and loads the kernel and modules specified there. (The /boot/loader.conf file contains the overrides to /boot/defaults/loader.conf, in a similar fashion to the way /etc/rc.conf works, which we will cover later in this hour.)

The loader counts down 10 seconds while it waits for a key press from you; if it doesn't get one, it boots the kernel in its default state. However, if you press Enter, it will put you into its command prompt interface in which you can control precisely your kernel boot procedure. You can boot in single-user mode (boot -s), boot an old kernel (boot kernel.old), boot from CD-ROM (boot -c), load and unload kernel modules one by one, view the contents of files (more), or perform a number of other tasks (see man boot for details). This should all be unnecessary most of the time. Usually, you will boot in the default configuration. Pressing ? at the ok prompt gives you a list of available commands, if you're curious. For further details on the options available at the loader command line, consult man loader.

This concludes the boot block phase of the bootstrapping process. We're now well on the way to bringing the system all the way up. The final phase of the boot process is where the complete FreeBSD system starts to come into play; where the kernel loads itself into memory, probes its available devices, and runs the "resource configuration" scripts that construct a working environment and start up the various system services.

- **kernel**. After loader transfers control, the kernel begins to probe all the devices it can find, and the results of each probe are echoed to the screen. This is the time when you will see many boot messages. These messages are logged in to the dmesg kernel buffer, which you can read with the dmesg command if you need to see what the kernel has to say about a certain device.

![](img/ba0161b65b37e94cffc801ecbacaba5e_131_0.png)

> `dmesg` is a fairly rudimentary tool, listing the contents of the system message buffer that have accumulated since the system last booted. Simply enter `dmesg` to view the list of messages or enter `dmesg | less` to view the output in an interactive pager for easier access.

- **init**. After the kernel loads, it passes control to the `init` process, the final stage in the startup procedure. This is signaled by the Automatic reboot in progress message, which involves `init` running the Resource Configuration script (`/etc/rc`). This script first checks all the filesystem devices in `/etc/fstab` for consistency, using the `fsck` (FileSystem Consistency check) program. If `fsck` finds no problems that it cannot correct on its own, it will mount all the filesystems (using `mount -a -t nonfs`) and continue running the rest of the startup processes. If `fsck` finds an unresolvable problem with the disks, it will exit to single-user mode for you to run `fsck` manually and repair the damage. Exit the single-user shell to continue rebooting into multiuser mode.

Finally, if all goes according to plan, you get a login prompt. This whole process usually takes no more than a minute.

## Resource Configuration Scripts

After `init` has been started, the remaining startup tasks in the system—the ones that start up all the services and operating system processes—are handled by the Resource Configuration scripts. These scripts can all be found inside the `/etc/rc.d` directory, which usually means “Resource Configuration Directory” (depending on who you ask).

Anything in `/etc/rc.d` is a resource configuration script, a program that starts up parts of FreeBSD according to the system’s configuration. Some are called recursively from other programs, some do nothing in the out-of-the-box configuration, and some will probably never even be run. You will generally never need to modify any of the files in `/etc/rc.d`.

A few other files are in `/etc`, however, that you will be modifying in order to configure your system. A list of some of the important resource configuration scripts that FreeBSD uses is shown in Table 7.1.

## TABLE 7.1 Resource Configuration Scripts

| Script Name | Description |
|---|---|
| `/etc/rc` | The main resource config script. |
| `/etc/defaults/rc.conf` | init reads in this file early to fill in its laundry list of tasks to do. |
| `/etc/rc.conf` | This is the file you edit to override defaults set in /etc/defaults/rc.conf. This should be the only resource config file in /etc that you edit. |
| `/etc/rc.d/diskless` | init reads this script if you're doing a diskless boot via BOOTP. |
| `/etc/rc.d/serial` | Sets up terminals and other serial devices. |
| `/etc/rc.d/pccard` | Runs the PC-card daemon for laptops. |
| `/etc/rc.d/network#` | Scripts that set up TCP/IP networking. |
| `/etc/rc.d/network_ipv6` | Same as rc.network, except for IPv6 services. |
| `/etc/rc.d/atm` | Called from rc.network; sets up ATM devices for WAN machines. |
| `/etc/rc.d/ipfw` | Called from rc.network; configures an ipfw firewall. |
| `/etc/rc.d/ip6fw` | Called from rc.network6; configures an ip6fw firewall. |
| `/etc/rc.d/devfs` | Configures the device filesystem. See Hour 10, "The FreeBSD Kernel and the Device Tree." for more on this file. |
| `/etc/rc.d/sysctl` | Sets kernel variables specified in /etc/sysctl.conf. |
| `/etc/rc.d/syscons` | Sets up console settings. |
| `/usr/local/etc/rc.d/` |  |
| `/usr/local/X11R6/etc/rc.d/` | Directory trees containing any new startup scripts you add (or are installed automatically by programs). |

## Modifying System Settings

The main resource configuration script, /etc/rc, is a completely automated "harness" that reads in a global configuration file and then executes a series of other scripts from /etc/rc.d in a specific order. Now that you know what the /etc/rc.d scripts do, we can look at how to configure the behavior of /etc/rc.

### The /etc/defaults/rc.conf File

The /etc/rc program is a shell script that operates based on the states of dozens of different variables. If a certain variable (for instance, sendmail_enable) is set to YES, /etc/rc will run the /etc/rc.d script that starts Sendmail. If the variable is set to NO, it does not run the Sendmail script.

FreeBSD is installed with a file that defines all the default states for all the variables that have meaning to /etc/rc. This file is /etc/defaults/rc.conf. The first thing /etc/rc does is to read in this file so that it knows what default assumptions to use for all its configuration variables.

Let's look at a typical block in /etc/defaults/rc.conf, shown in Listing 7.1.

### LISTING 7.1 Excerpt from /etc/defaults/rc.conf

```
# named. It may be possible to run named in a sandbox, man security for
# details.
#
named_enable="NO"      # Run named, the DNS server (or NO).
named_program="named"  # path to named, if you want a different one.
named_flags=""         # Flags for named
#named_flags="-u bind -g bind"  # Flags for named
```

By looking through /etc/defaults/rc.conf, you can find what /etc/rc will do unless you explicitly override it. In this case, you can see that the default behavior is to not run named at all.

### The /etc/rc.conf File

How do you override the default settings in /etc/defaults/rc.conf? You do it with /etc/rc.conf, which is read into /etc/rc immediately after it reads in the defaults. FreeBSD can operate just fine without an /etc/rc.conf file present at all; it's just a plain text file that you can create manually in a text editor, with one variable per line. You only have to add the variables to this file that you want to override so that your desired value is used instead of the default value. After you make configuration changes with sysinstall, certain variables related to those changes are written out automatically by that program into /etc/rc.conf. You can see what's in yours by using more /etc/rc.conf.

Let's say that we do want to run named. In the simplest case, all we would have to do is edit /etc/rc.conf (the overrides file) and add the following line anywhere in the file:

```
named_enable="YES"
```

The rest of the named_* variables in /etc/defaults/rc.conf do not need to be copied into the overrides file; remember, every variable in the defaults file is loaded into memory by init, and they only matter if the "master switch" for that block has been turned to "YES". If it has, the variables will be used in the execution loop in /etc/rc to launch whatever process is controlled by the block we're working on (in this case, named).
