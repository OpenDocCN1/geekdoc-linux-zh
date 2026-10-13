# The Basics of the FreeBSD Startup Process

When you first turn on your computer, a number of processes must occur before you can start using it. For example, your computer needs to check that all of its hardware is available and working properly, and load the instructions off the hard disk that tell it what to do next. A basic understanding of these processes is helpful for understanding how FreeBSD works, as well as for troubleshooting problems when things go wrong.

# The POST

The first thing that happens when you turn on your computer is called the *Power On Self Test* (*POST*). This is a program run by your computer’s *BIOS* (*basic input/output system*). During this stage of the startup process, the computer checks all of its hardware to make sure that everything is there and working. It counts the available RAM and performs some basic tests on it, determines the types and size of available media (hard disks, and so on), and assigns resources to plug-and-play devices. Note that this stage of the startup process has nothing to do with FreeBSD. This step is performed no matter what operating system you intend to start on your computer. At this point, your computer still doesn’t know anything about what operating system it will be running.

# The Bootstrap

After the POST has completed, your computer’s BIOS looks for a device on your system that it can load an operating system from. The order in which devices are checked for an operating system can usually be configured in your system’s BIOS setup menu. Oftentimes, the floppy drive is the first device that gets checked. This is why you get the “Non-systems disk or disk error” message if you have a floppy disk in your drive when you turn on your computer. Normally, the device that the system boots from will be the system’s hard disk.

# The Boot Manager

After the BIOS has found a bootable hard disk, it will read whatever is located at sector 0 on the hard disk. You can think of sector 0 as basically being the first thing on the hard disk. Sector 0 is also known as the *Master Boot Record* or *MBR*. This procedure begins what is called the *bootstrap*, which gets its name from the idea that the system is “pulling itself up by its bootstraps.”

If you installed a dual boot system so that you can choose whether you want to work in Windows or FreeBSD each time you start your system, the FreeBSD boot manager program is what will be located in the MBR. You will know that this stage of the boot process has completed when you get a menu that looks similar to the following: