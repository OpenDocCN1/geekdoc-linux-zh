# 24 · CHAPTER 3

productivity, especially if the server happens to be hosting an e-business application. And that might just cost you your job.

In the context of a Linux server, preparation includes the following steps:

+   1. Ensure that the hardware is supported by the operating system.
2. Ensure that the hardware has sufficient capacity for the tasks that you plan for it.
3. Determine what software you need for the server. (Most server software is bundled with the operating system, but you might need to gather some from additional sources. Ensure that you retrieve the documentation and software updates during your quest.)
4. Decide how to carve up the disk estate.
5. Plan your backup and recovery strategy.
6. Install, configure, and test.

Each of these steps is discussed in detail in the following sections.

# Is Your Distribution Compatible with Your Hardware?

As discussed in the previous chapter, hardware compatibility can be a major issue when selecting Linux as your operating system of choice, since it does not always support the latest gizmos and gadgets. Fortunately, the manufacturers of those products target the home user, where the "sizzle" factor sells more product than actual utility. Since you are building a server, you are dealing with an area where Linux excels and unsupported gizmos are unlikely to be a factor. You still need to do your homework, however, to ensure that you do not have nasty surprises during installation.

Highest on the compatibility checklist is the platform's architecture, on which you plan to install Linux. Unlike Windows, which runs only on Intel or compatible hardware (Windows NT does run on the DEC/Compaq Alpha chip, but is no longer supported), Linux is available on a number of different platforms. It is imperative that you get the distribution for your architecture. Because the focus in this book is on Linux-Intel-compatible platforms, you will need the Red Hat Distribution for the "x86" platform.

Next in priority is compatibility with disk interfaces. Two different interfaces are commonly in use. The first, SCSI (Small Computer System Interface), is typically used in server and workstation machines. SCSI has been around for a long time, and the equipment that you use is usually of high quality and reliability. SCSI has two main benefits: performance and compatibility. Except for the very low-end controllers with page scanners, SCSI controllers include their own processors. These processors handle the communications between the peripherals and the main system, which increases the performance of the system as a whole. At the time of this writing, the maximum transfer rate available for a SCSI-based system is 160 Mb/sec. Since SCSI has been around for such a long time, it's almost a foregone conclusion that the SCSI controller you want to use will just just fine with Linux, particularly if it's from a mainstream manufacturer.