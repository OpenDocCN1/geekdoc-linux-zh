
The halt command has several flags: `-n`, `-w`, `-d`, `-f`, `-i`, and `-p`. The `-n` flag prevents the sync call. It is sometimes necessary to halt the system in this way after repairing the root file system with `fsck`. The `-f` flag is used to bring the system down in a hurry. It does an immediate halt without syncing the file system, killing processes, or writing logs. This is not a recommended way to shut down a machine.

The `-w` flag does not halt the machine but only writes a `wtmp` entry. The `-d` flag prevents writing of the `wtmp` entry when halting the machine. The `-i` flag causes all network interfaces to shut down just before the halt. The `-p` flag tells `halt` to power off the machine after the halt.

## reboot

`reboot` is similar to `halt`, except that it causes the machine to reboot from scratch after halting. Using the `reboot` command is similar to running `shutdown -r`. The `reboot` command has the same flags as the `halt` command.

## CTRL+ALT+DEL

Another easy and safe way to shut down or reboot an x86-based Linux machine is to use the all-too-familiar Ctrl+Alt+Del key combination. This causes the following line in the `/etc/inittab` file to be processed by `init`:

```text
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

When you press Ctrl+Alt+Del, `init` runs the command `/sbin/shutdown -t3 -r now`. The shutdown starts immediately, as specified by the argument `now`. The `-t3` argument tells `init` to wait three seconds before sending the terminate signal to all processes. The `-r` argument tells the system to reboot after the shutdown.

> **Note**
>
> Sometimes it is desirable to disable the Ctrl+Alt+Del command to prevent accidental reboot of machines by novice users. To disable this command, change the line in the `/etc/inittab` file starting with the `ca:` entry to the following:
>
> After editing the `/etc/inittab` file, signal `init` to reread its configuration file with the `telinit` command as follows:
>
> `# telinit q`

## TROUBLESHOOTING

You might be faced with situations when a system will not boot successfully. This can be caused by hardware problems, file system corruption, an improperly configured newly built kernel, or by errors in startup scripts.

### Hardware Problems

If a certain piece of hardware has failed, it must be replaced. If the failed hardware is a disk drive, you will need to replace the disk, build a new file system, and then restore the files from backup tapes.

Bad memory chips are another possible cause of booting failure. In this case the task is to identify the bad chips, replace them, and then proceed to boot the machine.

Faulty power supplies can cause system failures. It is good to check the power supplies of each individual piece of equipment. Make sure cooling fans are working. Also check loose network cables, SCSI cables, and SCSI terminators. Make sure all disk drives are online. These things can seem obvious but are easy to overlook.

Sometimes just power cycling all the equipment will clear up boot problems. Turn power off to all equipment. Power up all peripherals and external disk drives first, and power up the CPU at the very end.

Finally, run hardware diagnostic programs that are suitable for your hardware to isolate problem areas.

Sometimes it is possible to avoid a catastrophic system failure by regularly checking system logs. Often a failing piece of hardware will start logging errors and, if caught early, you can schedule system downtime and replace it, thereby avoiding a major system crash and subsequent rebuild.

### File System Corruption

If a system goes down because of a sudden power failure, it can cause the file system to be corrupted. This can generally be corrected by booting the system in single-user mode and running `fsck` on all file systems.

You need to pay close attention to the boot-up messages. Any messages about inodes, superblocks, or other disk-related subjects suggest file system problems, and running `fsck` is the way to fix them. This, of course, assumes that you do not have a physically failing disk, in which case you must replace the disk and restore files from backup tapes.

### Newly Built Kernel Won’t Boot

When you build a new kernel, you can run into problems if the kernel was misconfigured, and the system can refuse to boot. When building new kernels, always make sure you create a backup LILO entry to boot the older kernel. An example of how you can specify alternate Linux boot images in `lilo.conf` was discussed in the LILO section earlier in this chapter.

Another way would be to boot using an emergency boot disk, mount the root partition on the hard disk, reconfigure and rebuild the kernel properly, and reboot using the newer fixed kernel.

## ERRORS IN STARTUP SCRIPTS

This is a common problem that is fortunately not hard to fix. What typically happens is that you add or make changes to startup scripts in `/etc/rc.d` and then you reboot; the system refuses to come up in multiuser mode.

The solution is to boot the system in single-user mode and look for the changes last made to the startup scripts, identify and fix any errors, and reboot your system.

![](img/6c13bcf02a08ad7923caab46f051d96a_87_0.png)

## CHAPTER 5

## USING *xdm* TO CREATE AN X WINDOWS APPLICATION SERVER

In this chapter:

- What Is an X Application Server? 72
- Using `xdm` to Create Linux-Based Logins for X Workstations and Terminals 73
- Troubleshooting 80

## WHAT IS AN X APPLICATION SERVER?

The X Windows System, the graphical environment for UNIX and Linux, offers the capability to display applications on remote hosts on the network. This means an application running on one host can be displayed and used interactively on another. The capability to distribute X applications, effectively separating the user interface from the processing, makes it possible to deploy X application servers.

An X Windows System application server is a system that accepts logins from X desktops (which can be special hardware X terminals) and then runs applications that are displayed on these desktops. Using this mechanism, you can deploy X applications on centrally managed servers and thus focus the hardware power for processing and running these applications in a few servers. This limits the need for powerful, complex hardware on the desktop.

This type of centrally managed application environment offers the promise of reduced total cost of ownership because desktops become essentially dumb graphical terminals, which do not need individual configuration and can easily be replaced when they fail.

## UNDERSTANDING THE RELATIONSHIP BETWEEN CLIENT AND SERVER IN THE X WINDOWS SYSTEM

When X applications are run remotely in the fashion just described, a strange thing happens: The terms client and server become confused and unclear. A distinction is made between the X application program and the X Windows System.

In the context of requesting and running an application, the user sits at a workstation that is the client from which a request is made to run an X application on a remote X application server. The application executes on the remote X application server, but its input is received from, and its output displayed on, the client workstation. This is quite straightforward because the client and server terms apply as they are normally understood.

However, in the context of the X Windows System environment itself, the terms are reversed. X consists of two components: the X server and the X client. The X server program runs on the client workstation and renders the graphical display of the application. The X application program is the client, issuing rendering commands to the X server program running on the client workstation. The X client program can be running on the local workstation or on a remote X application server. Notice how the client and server roles are reversed in the X Windows System context.

In the distributed X environment of an X Windows System application server, the X server runs on the client desktops and the applications, which are clients to these X servers, run on the X application server.

Therefore, the client terminal runs an X server and the X application server runs X applications, which are clients of the X server. The fact that the applications running on the X application servers are X clients actually is logical: The applications request the service of the
