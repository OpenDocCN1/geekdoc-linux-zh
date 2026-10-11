![](bbox=[0.07, 0.05, 0.78, 0.44])

the Linux boot process more digestible, we're going to break it down into the following phases:

+   - The BIOS phase
+   - The bootloader phase
+   - The kernel phase

Let's start by discussing the BIOS phase.

# ## The BIOS Phase

Regardless of what operating system you're using, when you first power on an x86 or x86-64 personal computer, the system BIOS is the first component to take charge of the boot process. The system BIOS is a ROM chip integrated in the motherboard that contains a series of very small programs and drivers that allow the CPU to communicate with basic system devices, such as the keyboard, I/O ports, the system speaker, system RAM, floppy disk drives, and hard drives. Variable information about your system, such as the amount of RAM installed, the geometry of your hard drives, and the type of floppy disk installed, are stored in the CMOS chip. The BIOS uses the data in the CMOS chip to address these devices.

The BIOS plays two key roles during the boot process. First, it tests the various system components and makes sure they are working properly. This is called the power-on self-test, otherwise affectionately known as POST. If the BIOS encounters any problems with system devices during POST, it will either display a cryptic error message on the