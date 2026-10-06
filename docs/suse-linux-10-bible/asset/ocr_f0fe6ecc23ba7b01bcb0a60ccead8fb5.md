# # THE RESC System

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