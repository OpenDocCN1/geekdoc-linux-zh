# 8 Chapter 2 • Linux Boot and Shutdown

different partitions and want to choose which one you want to boot, LILO will let you do this.

In addition, LILO allows you to send boot parameters to the kernel before it starts up, as the Sun architecture allows you to send boot parameters to Solaris. For example, you can specify root drive, what devices you have installed, and pass instructions to the *init* command.

# The Boot Prompt

When you start your machine after installing Linux, you probably have the LILO: prompt awaiting your command. At this point, you can choose to boot whatever operating systems were configured previously (Linux or DOS, example). If you're starting something like DOS or Windows 95, there isn't much you need to worry about, and you can just type "DOS" or "Win95" however you configured LILO when it was installed. If you forget, you can hit the TAB key to see a list of what operating systems LILO knows about will boot.

If you're starting Linux, there's a bunch of configuration parameters you can use at the end of the name you use to start Linux. For our example, let's say that we configured that name as "linux".

This signals Linux to use a different root partition than is configured in the kernel. When you build Linux on one system, it assigns a default of what the current root partition is. For example, if you build a Linux kernel on an SCSI-based machine where the root partition was the first drive, Linux will assign the boot device to /dev/sda. If you were to put this kernel on a floppy drive and use it to boot an IDE-based system, it would not boot correctly, since there is no system to boot off of. Adding in the root=/dev/hda1, for example, would tell the kernel to boot off of the first IDE drive, first partition. So, the same kernel can be used for multiple systems.¹

This signals Linux to mount the root filesystem in read-only mode. No changes can be made to the filesystem when read-only mode. The advantage of this is that the startup scripts can perform a filesystem check (fsck) to verify the integrity of the filesystem. If the fsck succeeds, the root partition is mounted read-write and normal boot continues. If there is a problem with fsck, the partition remains in read-only mode

¹ Assuming, of course, all the drivers that each system needs are installed.