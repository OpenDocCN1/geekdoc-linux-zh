
## STARTING UP AND SHUTTING DOWN

A command such as this verbosely checks the root file system as defined by your system setup (hence the -v) or / and corrects the errors. This command uses the default file system type of ext2 (the -t flag sets the file system type).

By the same token, the command `fsck` by itself and the file system name will accomplish the same purpose without the flags or options.

```bash
fsck /dev/hda1
```

The `fsck` command exists on other systems as well and can be used for a variety of other file system types. Consulting the man pages before executing any command involving `fsck` is always a good idea.

## Understanding Kernel Panics

In the case of a kernel panic, or when the boot sequence fails to load the kernel correctly and the machine cannot start correctly, you cannot do much to get the computer operative without making changes to the kernel. Upon bootup, an error message saying “Kernel Panic” will usually be followed by additional information stating what might have caused the system to halt. An error such as this indicates a bad kernel or one that cannot read the available options on the system or cannot read them as they are set up in the kernel.

Several things can cause a kernel panic. Often such a panic results from a customized kernel that was built without some necessary content. When building any sort of custom kernel, it is best to have a backup kernel in case things go wrong. A reboot to the previous kernel will usually solve the problem until a properly configured kernel can be compiled.

Improperly loaded kernel modules can also cause a kernel panic, whether they are for a SCSI device, an improper file system type, or loss of disk partitions. It is always wise to keep some sort of backup handy for cases when the system goes down or when the system does not reboot normally. The best thing to do in these instances is to attempt to reboot the machine with another kernel, whether it be the default or a backup. You can also use the Red Hat boot disk to gain a root prompt or create a Linux rescue disk during the installation routine. If you can get to a root prompt in any manner, then you should be able to correct the problem. I suggest taking enough precautions by adding *golden kernels*, or kernels that have proven trustworthy, and by editing the `/etc/lilo.conf` file to allow for backup options. If none of these alternatives are available, a most unlikely scenario, a reinstall may be your only choice. I have found it easier in the long run to attempt to resuscitate a bad box than try to reconstruct one via a reinstall. Not much can be done, however, in the event of a bad kernel and no backups except to create a new one or use an older, stable kernel release.

## Checking for Hardware Errors

In the case of damaged hardware, before you start tearing your machine apart and replacing components looking for the source of the error, make sure the error is hardware-related. If you consistently get an error message pertaining to memory or related signal 11 errors, it is a safe bet that the fault in fact lies with the hardware. But check through some of the possible options before tinkering with the hardware. You might just end up making a bad problem worse, especially if you are unsure about what you are doing.

Here are some possible solutions to try before replacing what you may think are defective parts:

- Make sure that all the computer parts are receiving power. This may be an obvious solution, but it is surprising how often you forget to plug power into the various drives. As embarrassing as it may be, I have forgotten to plug in hard drives and then been unable to power them up.
- Verify that the cables are plugged properly. It is easy on some of the older ribbon cables to place the one-pin or the colored stripe on the cable improperly. Most cables now have a corresponding tab on the end that fits into a similar notch on the drive.
- When installing new parts, first make sure they are compatible—that is, make sure that Linux supports this type of hardware. USB and DVD support is still under development for Linux, so don't plug in a USB scanner or WinModem and then get frustrated when it doesn't work immediately.
- If some of the installed cards are jumpered, try changing the jumpered settings so there are no conflicts. This was true with an old Adaptec SCSI card I recently came across and installed on my system. Fortunately, the different settings for setting the jumpers or by shorting the pins on the card were printed on the device itself. Also, it never hurts to take a look on the Internet for a more detailed printout of the card's settings. In this particular instance, I needed to turn off a certain jumper so that it would not conflict with the floppy drive.
- Check the lights on the equipment. If the network card, for example, is not lit, the card itself may be either defective or conflicting with another card.
- Try shutting the machine down completely and then restarting it. This clears any random errors from RAM and resets the machine to a known default state. This whole procedure is a bit too reminiscent of working with Windows, but it sometimes proves effective.
- If the machine booted correctly once before, be sure to note the place in which the current boot procedure now hangs. A simple comparison between the two can usually determine what piece of hardware is causing the error.
- Linux provides various diagnostic tools in case of hardware failure. Using one of the available boot disks and then mounting the Linux CD will give you a shell in which you can then start probing the hardware.
- At the LILO: prompt, try typing `linux single` to boot into single-user mode. This will grant you a root shell and allow access to the system without network interference.

If after trying these options you still cannot locate or diagnose the problem, then try installing either different hardware or swapping out the existing parts with known functional hardware. The worst-case scenario is to purchase either older parts or purchase newer compatible equipment. As more and more manufacturers cater to the Linux crowd, hardware will soon become standardized on the Linux platform.

## Testing the System

If you succeed in reaching a login prompt, either by resetting some of the hardware or by using one of the boot CDs, it is a good idea to make sure the system is indeed functioning correctly. One of the directories on the system that keeps track of hardware is the `/proc/` directory. Here you can usually see what the settings are for various items installed on the machine. For instance, to test for available memory, try using this command:

```bash
cat /proc/meminfo
```

The `cat` command is very useful for printing out the contents of a certain file without having to open the file with a text editor. The `/proc/` directory is also very unique in that the contents are in a dynamic state and are created on demand by the kernel depending upon the state of the system. None of the files here are static, but only exist in a temporary state while the machine is operational. Several other files in this directory also give additional information about various items. Some worth noting are `cpuinfo`, `interrupts`, `ioports`, and `partitions`. A thorough perusal of this directory will reveal additional items of interest.

Another directory to be aware of is the `/dev/` directory. Here you can find not only information about the different hardware devices, but also a nifty utility called `sndstat`. This utility reports the status of the sound card. To use this utility, type the following:

```bash
cat /dev/sndstat
```

This utility identifies the installed sound drivers and the IRQ assigned to the sound card. It also lists the card's configuration and all the audio, synthesizer, midi, mixer, and timer devices. Listing 2.7 shows sample output.

### Listing 2.7 Sample Output from the sndstat Utility Listing Sound Card Information

```
# cat /dev/sndstat

OSS/Free:3.8s2+--971130

Load type: Driver loaded as a module

Kernel: Linux Linux pluto 2.2.16 #1 Wed Jun 14 00:51:03 MDT 2000 i586

Config options: 0

Installed drivers:

Card config:

Audio devices:

0: Sound Blaster Pro (8 BIT ONLY) (3.02)

Synth devices:

0: Yamaha OPL3

Midi devices:

0: Sound Blaster
```
