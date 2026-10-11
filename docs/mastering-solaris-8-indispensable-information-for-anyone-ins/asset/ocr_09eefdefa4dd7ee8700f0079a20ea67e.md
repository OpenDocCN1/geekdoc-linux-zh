server and you need to define a new device alias, this command will show you the physical device path to your disks. You can then copy and paste the output to make a new device alias.

**show-displays**  Shows the physical device path to the frame buffer. The frame buffer is what puts out the graphical display on a Sun server. Most likely, this command will be used only by Sun field engineers and Sun support teams.

**show-nets**  Shows the physical path to network devices. The network devices are one or more network cards.

**show-post-results**  Shows some detailed output of the POST test. The output can be seen only if critical hardware is still available. If a simple device such as a modem goes out, it will be indicated in the output. If a critical piece of hardware such the CPU goes out, the only way of detecting it is with the system LEDs.

**show-sbus**  This command works only on older systems that have the SBUS architectures. Newer systems don't even have this command in the NVRAM chip.

**show-tapes**  This is just like the other show commands. This command might not pick up on third-party solutions that do not use the interface.

There is another command called test. It will run diagnostics on devices that have hardware-level diagnostic test routines built in. If a device is driven by software device drivers for hardware operations (such as moving the disk heads), this command might not work or it might produce limited results. Most Sun peripheral equipment will respond to the test command. The format is test device-alias. You can also use test-all to test everything. It is fun the first time and can be useful if the system is acting flaky.

If you have to contact Sun for hardware support, the support team member will most likely ask you to run the OK command. .version This command displays the OBP and POST firmware versions for your server. The most common OBP versions are 2.x and 3.x. OBP version 1.0 was in use around the early 1980s and is extremely rare if it can be found at all. Most current servers support firmware upgrades from software. The support representative might ask you to download the latest hardware firmware for your server and upgrade the firmware before continuing with the hardware trouble-shooting session.

There are some probe and show commands that require the system to be reset before they can be used:

+   1. First have the system at the OK prompt.
+   
+   2. Then use the command setenv to set the variable auto-boot? to false.
+   
+   3. Now type the command reset-all.