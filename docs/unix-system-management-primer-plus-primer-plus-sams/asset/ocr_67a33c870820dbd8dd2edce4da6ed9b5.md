It is important to revisit the disk space situation—after the upgrade is complete; many upgrade procedures ask for more space than is necessary—just to be safe—and only need the extra space for staging the installations. If, after the migration, you find that the original file system has enough space to store the data you migrated, move the data back to its original location as soon as possible. Storing the files in their original file system avoids cluttering other file systems or partitions that you used if you created a new system.

# Ensuring Adequate Driver Support on the Upgraded Operating System

If you've ever hooked up a disk array, tape drive, or printer to your system, chances are that you've installed or used a device driver. Drivers are also used to enhance the kernel with features like new file systems and unsupported network protocols.

Because drivers are the link between the kernel and devices, they show a great affinity for the kernel under which they were developed. A network card driver built for the Linux 2.2 kernel will probably not work on Linux 2.4 without recompilation and possibly some code changes.

Broken drivers can bring an upgrade to a grinding halt. If the operating system can't talk to the hardware it's running on, there's really nothing a system administrator can do to solve the problem, short of writing for his or her own drivers.

Luckily, most developers and hardware vendors have early access to new releases of operating system, and can have new drivers ready in time to supplement the general release of the new operating system version. If everything works out, these new drivers prevent the driver incompatibility from occurring. If you have to build your own drivers, make sure you verify the vendors release schedule, so you have time to get the drivers ready before your upgrade.

# Firmware Upgrades

Many novice computer users (and beginning system administrators) are surprised to learn that hardware such as network cards, disk drives, and motherboards come with their own software, and they require that software in order to work at all. Firmware is the term used for software that has been written into ROM (read only memory) and that accompanies a specific piece of hardware.

# The BIOS Is Firmware

One type of firmware that most people are familiar with is the BIOS (basic input/output system) on PCs. The BIOS is software that contains all the code necessary to run the PC's keyboard, disk drives, monitor, drivers, and other critical functions. The BIOS comes from a ROM chip. On most motherboards, BIOS resides in flash ROM—a ROM chip that can be reprogrammed, or "flashed," with a new version of the BIOS. Flash ROM retains its settings through shutdowns and reboots, so it's perfect for running an application like the BIOS.

![](bbox=[0.133, 0.788, 0.203, 0.843])