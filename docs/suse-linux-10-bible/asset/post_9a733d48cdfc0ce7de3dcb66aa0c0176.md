
◆ Paragon Mount Everything (www.mount-everything.com/) — Mounts EXT2 and EXT3 filesystems under Windows 9x, NT, 2000, and XP. Paragon Software Group's home page is at www.paragon-gmbh.com.

We highly recommend Explore2 as an open source solution and Paragon Software Group's Mount Everything as a commercial solution. Many people have reported success with the other packages listed in the previous list, but we have no direct experience with them.

## Troubleshooting Booting

Unfortunately, an important part of system administration is fixing problems, and the authors have spent many hours fixing configuration problems for customers. This section explores what to do if you have trouble booting your system.

## Fixing Boot Problems Using Runlevels

We discussed runlevels earlier in this chapter, and if you have a corrupt system, or a runaway process that is loaded in the init process, one way to fix this is to force the system into a specific runlevel to stop that process from running. This is achieved by passing runlevel number to the boot loader at time. LILO and GRUB are capable of passing parameters to the kernel before it is loaded, which is a feature that every Linux user should know how to use.

The kernel is able to take parameters in the same way that a normal application or program can. To do this, the kernel must know this information before it is loaded and executed so that it can make changes based on what you need to. The kernel itself does not deal with runlevel systems up. Init is defined in the /etc/initab file by default, it can be overridden from the boot manager. The feature of the kernel that allows this is that any parameter you pass will be understood by the first process that the kernel calls after its initialization. In the case of Linux, this is the init process. If you remember, the way to change a runlevel is to use the init process with the runlevel as a parameter. If you add the runlevel number to the kernel command line before booting, this number is sent to the init process, which boots the system into the specified runlevel.

To pass an init parameter to LILO, you can specify linux 1 on the LILO prompt to load up the boot profile called Linux.

In GRUB you do this by selecting the profile you would like to edit and entering the number of runlevel into which you want to enter at boot (see Figure 4-3).

In both cases, the 1 tells to load up the system in runlevel 1. This, as you may remember, the runlevel that signifies single-user mode with no network. This is the lowest usable runlevel that is needed only if there is a problem with the system.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_175_0.png)

**Figure 4-3:** Adding the runlevel to the GRUB boot loader

As shown in Figure 4-4, you will be asked for the password to log in the system (this is why you should *never* forget your root password). Once logged in you can then off processes as we talked about with the `chkconfig` script or fix any other problems the system has. Once fixed, you can then reboot the system normally. Because specifying a runlevel to GRUB and LILO is a temporary change, you are able to let the system start up normally without having to interrupt the normal operation of LILO or GRUB.

## THE RESC System

We have talked about fixing problems by changing the runlevel of the system temporarily, but what if you encounter a dire problem such as forgetting the root password? This requires another approach because you will need the root password at some time.

```
dev/sdb1 on media/floppy type subfs (rw,nodos,nodev,sync,fs=floppy,proc,id)  done
Loading required kernel modules  done
Restore permissions  done
Activating remapping devices in /etc/fstab...  done
Setting up the clock  done
Setting up timezone  done
Setting up licenses  done
Setting up hostname  umused
Setting up loop interface  done
  lo IF address: 127.0.0.1  done

Cleaning up -vsh/modify_resolconf/  done
restored /etc/resolv.conf from /etc/resolv.conf
enabling flood protection  done
Disabling firewall  done
Creating new-boot-msg  done
System Control: The system has been  done
Skipped features  set up
System Boot Control: Running /etc/init.d/local  boot.sched
IMIT: Entering locals...\done
Boot logging started on /dev/tty0(console,local) on May 24 10:22:17 2084
Master Resource Control (runlevel N): Switching to locals...\done
Hotplug is already active (disable with MOUNTFLAG=1 at the boot point)\done
scoldspawn image  done
scanning usb: --  done
scanning usb:  done

hci-hcd hci-hcd hci-hcd us-usb us-hci  done
Loading hardware quartop.gp  done
Start Unicode mode  done
Sending all processes the TERM signal...  done
Sending all processes the KILL signal...  done
IMIT: Going single user  done
IMIT: Sending processes the TERM signal  done
Terminated  done
Give root password for login:
```

Figure 4-4: Logging in to init 1

SUSE needs to be able to enable a Linux system, which generally requires Linux tools and has included a Rescue System on the first CD or DVD of your SUSE installation set. To load the Rescue System, use the optical media, and select Rescue System from the initial boot menu. The kernel from CD will load, and an initial ramdisk containing a fuller system will be loaded. This Rescue System has built-in support for the types of Linux filesystems discussed in this book, as well as IDE hard drives. If you are using a SCSI disk, this ramdisk also includes the modules for loading a SCSI disk.

## Chapter 4 ✦ Booting the System 133

As an example of using the SUSE Rescue System, we will take the case of a forgotten root password and reset this with the Rescue System.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_177_0.png)

Some of you might see a large security problem with what we are about to do. If malicious users have physical access to a server, they are quite able to reset the root password of the machine using this method. This is why the physical security of a machine is as important as the security of the machine from an operational standpoint.

To reset the root password from the SUSE Rescue System, follow these steps:

- 1. When the Rescue System has loaded, you will be prompted to select the keyboard map that you are using (which defines the type of keyboard that you are using). After the kernel executes, loads the initial ramdisk, and starts various system processes, you will then be asked to log in. Just enter **root** as the username, and you will be dropped into the Linux system from the initial ramdisk.
- 2. At this point, you need to identify the partition that contains /etc. This will usually be your / (root) partition. Mount the partition under /mnt. The following example uses /dev/hda3: `mount /dev/hda3 /mnt`
- 3. When mounted, you need to edit the file /mnt/shadow to reset the root password. You can edit this file using any text editor, although vi is the only screen-oriented text editor that is provided in the SUSE Rescue System. Remember that you have mounted your root partition under /mnt; this is the location of the /etc/shadow file has changed.
- 4. When loaded, you need to find the entry for the root user. The encrypted password, which is the second field (fields in the file are separated by a colon). When found, delete the password so that there are just two colons next to each other (:); save the file.
- 5. After the file has been edited, change the directory to / (root) and unmount the filesystem by issuing the: `mount /mnt`
- 6. When unmounted, you can reboot the system by typing **reboot** and pressing the Enter key, or just pressing the reboot key on the machine. Remember to remove your optical media as the system reboots, or you may accidentally boot from it.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_177_1.png)

You will find that you can log in to the system as root without a password. As soon as you are logged in, set the password immediately—and try to remember it.

The Rescue System is something every administrator and user should have in his or her arsenal as it can help you fix pretty much any lethal problem you have on a Linux system, regardless of whether it is SUSE-based or not.
