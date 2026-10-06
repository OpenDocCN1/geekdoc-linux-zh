# Understanding the Boot Process

Look for Hardware Type Names Many boot messages, particularly in the kernel ring buffer, relate to hardware. Searching for the name of the hardware type, as SCSI or USB, if you're having problems with these subsystems. Remember that Linux treats many disk devices as SCSI disks, too!

Look for Hardware Chipset Names Linux drivers log messages along with their drivers names, which are usually based on the chipset in. If you know your hardware well enough to know the chipset name, search for it or a subset of it. For instance, searching for 8169 may turn up messages to a RealTek8169 Ethernet interface. Similarly, you can search for higher-level kernel module names, such as reiserfs for messages from the ReiserFS filesystem driver.

The Study from a Working System Familiarize with the contents of the kernel ring buffer and log files if you expect a system is functioning correctly, you'll find it easier to identify problems when they occur.

Sometimes, a system won't boot at all. In this case, kernel boot messages (which ordinarily go into the kernel ring buffer) are displayed on the screen, which can help you identify the cause of a failure. Modern Linux distributions hide these messages by default, but you can reveal them by pressing the Esc key during the boot process. Once the kernel process has completed, other systems take over, and the last few messages displayed on the screen can provide clues—instance, if the last message mentions starting a particular server, it's possible that the server is hanging or chainloads interrupting the boot process. You may be able to disable the server using a single-user boot mode and bypass the process.

# The Boot Process

The process of starting an x86 computer from its initial state when the power is turned on to having a working operating system is complex because of the modern personal computers have evolved. The steps a computer goes through order to boot an operating system are follows:

+   1. The system is given power, and a special hardware circuit connects the CPU to load a predetermined address and execute the code in that location. The firmware (BIOS or EFI) resides at that location, so the CPU runs the firmware.

+   2. The firmware performs tasks. These include checking for hardware, configuring hardware, and looking for a boot loader.

+   3. When the boot loader takes over from firmware, it loads the kernel or chainloads to another boot loader, described earlier in this chapter.

+   4. Once the kernel takes over, it performs tasks as initializing devices, mounting the root partition, and finally loading and executing the initial program for your system. By default, this is the program /bin/init.

+   5. The initial program gets the process ID (PID) of 1 because it's the first program to run on the system. In a traditional Linux boot system, /bin/init reads the /etc/initt